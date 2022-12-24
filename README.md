
# Edit Information Using jQuery-AJAX on Modal using data-id.

In this work we will edit Information using jQuery AJAX on a Modal.
Specially we will do 'Select' & 'Radio' button on selected when we do Edit.



## File management

- In Modal we will pass database 'ID' with HTML Class/ID when we click on it.
```bash
Button :

  <p>Bill to the same address <a href="#" id="billing_id" data-id = {{$address->id}} 
  class="text-decoration-none text-primary"data-bs-toggle="modal"  
  data-bs-target="#staticBackdropforBillingAddressEdit" >Edit</a></p>
```

- Than we will write jQuery-AJAX code on <script> ... </script> (If blade file) or you can write this code on .js file.
```bash
  jQuery(document).on('click','#billing_id',function(event)
  {
        event.preventDefault();
        var billing_id = jQuery(this).data('id');
        $.ajax({
                url     : "{{ route('billing_address') }}",
                type    : 'GET',
                dataType: 'json',
                data    : {
                    id : billing_id,
                },
                success : function(response){
                    console.log(response.billingAddress.id);
                    jQuery('#bill_contact_person_name').val(response.billingAddress.contact_person_name);
                    jQuery('#bill_phone').val(response.billingAddress.phone);
                    jQuery('#bill_address').val(response.billingAddress.address);
                    
                    if (response.billingAddress.address_type === 'office') {
                        $('#bill_address_type_office').prop('checked', true);
                    }
                    else{
                        $('#bill_address_type_home').prop('checked', true);
                    }
                    $("#bill_city").val(response.billingAddress.city).change();
                    $("#bill_zip").val(response.billingAddress.zip).change();
                    jQuery('#billingAddress_id').val(response.billingAddress.id);
                },
        });
    });
```

- Than go to Controller write Query and send it to response.
```bash
  public function billing_address_edit(Request $request)
    {
        $id=$request->id;
        $billingAddress = BillingAddress::findOrFail($id);
        return response()->json([
            'billingAddress' => $billingAddress
        ]);
    }   
```

## Screenshots

![App Screenshot](https://via.placeholder.com/468x300?text=App+Screenshot+Here)

