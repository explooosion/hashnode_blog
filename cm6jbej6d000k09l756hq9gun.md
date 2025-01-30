---
title: "ASP.NET - RowCommand Find Control [VB]"
seoTitle: "ASP.NET - RowCommand Find Control [VB]"
seoDescription: "asp.net [VB]  筆記之 GridView 應用，請安心服用。"
datePublished: Mon May 16 2016 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbej6d000k09l756hq9gun
slug: aspnet-rowcommand-find-control-vb

---

asp.net \[VB\]  筆記之 GridView 應用，請安心服用。

GridView 中，常常在點擊按鈕事件後，要抓取該列中的控制項值。

範例情況：

 在 GridView 中，點擊 Button 後，取得列中 DropDownList 之 value

步驟程序：

RowCommand → Get RowIndex → FindControl → SelectedValue

1.本次事件建立於 RowCommand 中 

```vbnet
Protected Sub grid_RowCommand(sender As Object, e As GridViewCommandEventArgs) Handles grid.RowCommand

End Sub
```

2\. 利用 CType 取得該按鈕，並利用 NamingContainer 取得其父容器（GridViewRow），再指定 RowIndex

```vbnet
Dim rowIndex As Integer = CType(CType(e.CommandSource, Button).NamingContainer, GridViewRow).RowIndex
```

3\. 從 GridView.row(索引) 中取得控制項 FindControl

```vbnet
Dim ddl As DropDownList = grid.Rows(rowIndex).FindControl("ddl")
```

4.取得 DropDownList 選取之項目值

```vbnet
Dim _value As String = ddl.SelectedValue
```

有勘誤之處，不吝指教。ob'\_'ov