---
title: Autogenerated Fields
page_title: Autogenerated Fields
description: Autogenerated Fields
slug: raddataform-autogenerated-fields
tags: autogenerated,fields
published: True
position: 1
---

# Autogenerated Fields

Generally, the RadDataForm creates its fields automatically based on the type of the corresponding properties. Thus the proper editor controls are text fields for string properties, CheckBoxes for Boolean, DateTimePickers for dates, ComboBoxes for enums.

#### __Figure 1: Autogenerated fields__

![Autogenerated fields](images/RadDataForm_bindToCollection.png)

However, you are free to change each of the fields displayed. What you need to do is to set the AutoGenerateFields property of the RadDataForm to **True** and handle the **AutoGeneratingField** event. As it is cancelable, you may reject the cretion of a particular field.  

The arguments of the **AutoGeneratingField** event are:

* **Cancel**: Gets or sets a value that indicates whether the operation should be cancelled.

* **DataField**: Gets or sets the data field; it is of type DataFormDataField and depends on the type of the corresponding property. It can be:

	* **DataFormCheckBoxField**: Used for editing of boolean properties.

	* **DataFormComboBoxField**: Used for editing by choosing a value from predefined data source.

	* **DataFormDataField**: Used for editing of string properties.

	* **DataFormDateField**: Used for editing properties of type DateTime.

* **PropertyName**: Gets or sets the property name of the corresponding field.

* **PropertyType**: Gets or sets the property type of the corresponding field.

The AutoGeneratingField event will be fired for each current item, thus enabling you to customize the view on item basis. 

So, for example, let us decide on defining a Description for the Salary property, set the Label of the first property to be "First Name" and define purple foreground color for the ladies and a blue one for the gentlemen:

#### __[C#] Example 1: Handling the AutoGeneratingField Event__

	{{region cs-raddataform-autogenerated-fields_0}}
	private void DataForm1_AutoGeneratingField(object sender, Telerik.Windows.Controls.Data.DataForm.AutoGeneratingFieldEventArgs e)
	{
	    var employee = this.DataForm1.CurrentItem as Employee;
	    if (e.PropertyName == "FirstName")
	    {
	        e.DataField.Label = "First Name";
	    }
	    if (e.PropertyName == "Salary")
	    {
	        e.DataField.Description = "This is the initial salary!";
	    }
	    if (employee.Gender == Gender.Female)
	    {
	        e.DataField.Foreground = new SolidColorBrush(Colors.Purple);
	    }
	    else
	    {
	        e.DataField.Foreground = new SolidColorBrush(Colors.Blue);
	    }
	}
{{endregion}}

#### __[VB.NET] Example 1: Handling the AutoGeneratingField Event__

	{{region vb-raddataform-autogenerated-fields_0}}
	Public Sub DataForm1_AutoGeneratingField(sender As Object, e As Telerik.Windows.Controls.Data.DataForm.AutoGeneratingFieldEventArgs)
	    Dim employee = TryCast(Me.DataForm1.CurrentItem, Employee)
	    If e.PropertyName = "FirstName" Then
	        e.DataField.Label = "First Name"
	    End If
	    If e.PropertyName = "Salary" Then
	        e.DataField.Description = "This is the initial salary!"
	    End If
	    If employee.Gender = Gender.Female Then
	        e.DataField.Foreground = New SolidColorBrush(Colors.Purple)
	    Else
	        e.DataField.Foreground = New SolidColorBrush(Colors.Blue)
	    End If
	End Sub
{{endregion}}

Once you run the application, you should see the following:

#### __Figure 2: Result of customizing the autogenerated fields__

![Result of customizing the autogenerated fields #1](images/RadDataForm_customizeAutoGeneratedFields.png)
![Result of customizing the autogenerated fields #2](images/RadDataForm_customizeAutoGeneratedFields2.png)

## See Also

* [AutoCommit]({%slug raddataform-auto-commit%})