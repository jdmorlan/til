You can remove conditionals from your code, by creating a Null Object for instances where 
an object returned would be nil. 

```
# app/controllers/invoice_controller.rb

class InvoiceController < ActionController::Base 
  def show 
    @invoice = Invoice.find(params[:id]) || EmptyInvoice.new
  end
end
```

The `Invoice Controller` show action returns the invoice if it is found, but if it does not find an invoice 
it returns an object that mimics a Invoice with no data. 

```
# app/models/empty_invoice.rb

class EmptyInvoice 
  def line_items 
    []
  end
end
```

The only method on an invoice that may have problems is `line_items`, so the `EmptyInvoice` object 
returns an empty array for the method. Now there is no need for a conditional in your view. 

```
# app/views/invoices/show.html.erb

<div class="invoice-container">
  <% @invoice.line_items.each do |line_item| %>
    <p><%= line_item.description %></p>
  <% end %>
</div>
```

If no line_items exist for the invoice, there is no error because the `EmptyInvoice` object returns 
an empty array, versus nil. 

For more information, check out the talk by Sandi Metz on this pattern and many others: 

[Nothing is Something](https://www.youtube.com/watch?v=OMPfEXIlTVE)
