# How to get the reference of the control added inside the DataTemplate of the GridTemplateColumn in WPF DataGrid (SfDataGrid)?

## About the sample

This sample illustrates how to get the reference of the control added inside the DataTemplate of the GridTemplateColumn in WPF DataGrid.

[WPF DataGrid](https://www.syncfusion.com/wpf-controls/datagrid) (SfDataGrid) provides support to load any WPF control in the display mode for all columns by using [GridTemplateColumn](https://help.syncfusion.com/cr/wpf/Syncfusion.UI.Xaml.Grid.GridTemplateColumn.html). You can get the reference of the control which is added inside the DataTemplate of the GridTemplateColumn by selecting the cell. Here an example is shown to get the reference of the TextBox which is added within the GridTemplateColumn. 

```C#

private void OnButton_Click(object sender, RoutedEventArgs e)
{
    var columnElement = this.dataGrid.SelectionController.CurrentCellManager.CurrentCell.ColumnElement as GridCell;
    var dataColumn = columnElement.ColumnBase as Syncfusion.UI.Xaml.Grid.DataColumn;
    if (dataColumn.Renderer.GetType() == typeof(GridCellTemplateRenderer))
    {
        ContentPresenter contentPresenter = this.FindVisualChild<ContentPresenter>(columnElement);

        var TextBox = GetVisualChild<TextBox>(contentPresenter);
    }
}

private T GetVisualChild<T>(DependencyObject parent) where T : Visual
{
    T child = default(T);
    int numVisuals = VisualTreeHelper.GetChildrenCount(parent);
    for (int i = 0; i < numVisuals; i++)
    {
        Visual v = (Visual)VisualTreeHelper.GetChild(parent, i);
        child = v as T;
        if (child == null)
        {
            child = GetVisualChild<T>(v);
        }
        if (child != null)
        {
            break;
        }
    }
    return child;
}
public childItem FindVisualChild<childItem>(DependencyObject obj) where childItem : DependencyObject
{
    for (int i = 0; i < VisualTreeHelper.GetChildrenCount(obj); i++)
    {
        DependencyObject child = VisualTreeHelper.GetChild(obj, i);
        if (child != null && child is childItem)
            return (childItem)child;
        else
        {
            childItem childOfChild = FindVisualChild<childItem>(child);
            if (childOfChild != null)
                return childOfChild;
        }
    }
    return null;
} 

```

KB article - [How to get the reference of the control added inside the DataTemplate of the GridTemplateColumn in WPF DataGrid (SfDataGrid)?](https://www.syncfusion.com/kb/12548/how-to-get-the-reference-of-the-control-added-inside-the-datatemplate-of-the)

## Requirements to run the demo

Visual Studio 2015 and above versions
