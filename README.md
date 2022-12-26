
# Insert with form validation and Edit Information Using jQuery-AJAX on Modal using data-id.

In this work we will edit Information using jQuery AJAX on a Modal.
Specially we will do 'Select' & 'Radio' button on selected when we do Edit.



## File management

- In Modal we will pass database 'ID' with HTML Class/ID when we click on it.
```bash
Button :

  <p>address <a href="#" id="id" data-id = {{$address->id}} 
  class="text-decoration-none text-primary"data-bs-toggle="modal"  
  data-bs-target="#staticBackdropforAddressEdit" >Edit</a></p>
```

- Than we will write jQuery-AJAX code on <script> ... </script> (If blade file) or you can write this code on .js file.
```bash
  jQuery(document).on('click','#id',function(event)
  {
        event.preventDefault();
        var id = jQuery(this).data('id');
        $.ajax({
                url     : "{{ route('billing_address') }}",
                type    : 'GET',
                dataType: 'json',
                data    : {
                    id : id,
                },
                success : function(response){
                    console.log(response.billingAddress.id);
                    jQuery('#id').val(response.Address.name);
                    jQuery('#id').val(response.Address.phone);
                    jQuery('#id').val(response.Address.address);
                    
                    //radio-button
                    if (response.billingAddress.address_type === 'office') {
                        $('#bill_address_type_office').prop('checked', true);
                    }
                    else{
                        $('#bill_address_type_home').prop('checked', true);
                    }
                    
                    //select-option 
                    $("#bill_city").val(response.billingAddress.city).change();
                    $("#bill_zip").val(response.billingAddress.zip).change();
                    jQuery('#billingAddress_id').val(response.billingAddress.id);
                },
        });
    });
```

- Than go to Controller write Query and send it to response.
```bash
  public function address_edit(Request $request)
    {
        $id=$request->id;
        $val = Model::findOrFail($id);
        return response()->json([
            'billingAddress' => $val
        ]);
    }   
```

- Insert Data using ajax with form validation(use validation cdn) : 
```bash
  $.validator.setDefaults({
            success: "valid"
        });

        $("#AddressForm").validate({
            rules: {

            },
            messages:{

            },
            unhighlight: function(element, errorClass, validClass) {
                $(element).next('label.error').remove();
            },
            submitHandler: function(form) {
                $.ajax({
                    url: "{{route('route-name')}}",
                    type: "POST",
                    data: $('#AddressForm').serialize(),
                    success: function(data) {
                        window.location.reload();
                    }
                });
                return false;
            }
        });   
```

## Screenshots

![App Screenshot](https://via.placeholder.com/468x300?text=App+Screenshot+Here)

