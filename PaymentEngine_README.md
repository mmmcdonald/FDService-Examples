# Payment Engine

In the Fonteva Services platform developers can extend/overwrite the callouts to the payment processor.  
This section will outline different ways to to use the Payment Engine. 

1. ##### Gateway Specific Fields (Level 2 or Level 3 Processing)
    With Spreedly to send extra information to the gateway you have to use Gateway Specific Fields. These
    fields can differ from gateway to gateway. [Spreedly Gateways](https://www.spreedly.com/all-gateways]) will 
    outline what those fields are. This is also how Level 2/Level 3 processing is supported. To do this look at 
    the class [PaymentService_GatewaySpecificFields](PaymentEngine/main/default/classes/PaymentService_GatewaySpecificFields.cls).<br/>
    This class should extend the FDService.PaymentService and overwrite all methods that need these specific fields.
    These methods will be auto called when the Fonteva Platform calls them during the normal purchase process.
1. ##### Custom Gateways That Spreedly Does Not Support
    Some gateways are not supported by Spreedly and this will requires the ability to connect the Fonteva Platform 
    to the gateway. The same class would be overwritten as for gateway specific fields however more methods 
    would need to be updated. All methods that would be required will need to be updated. As long as the response
    from each method is in the form of FDService.EPayResponse the rest of the platform should create all supporting
    records. Inside the FDService.EPayResponse there is a object that is FDService.EPayTransaction, this object
    is where the response from the gateway will be mapped to. As control is returned to the Fonteva Platform the 
    FDService.EPayTransaction will be mapped to EPayment records which will drive the Receipt/Transactions etc.
    ([PaymentService_CustomGateway](PaymentEngine/main/default/classes/PaymentService_CustomGateway.cls)) This example
    is a fully operation integration with Stripe. It will allow purchase via our payment page and
    all for processing refunds. It will work with Scheduled Payments internally without any modification.
    
    This example of custom gateway also includes the AliPay/WeChat flow for Stripe. A custom payment
    type example is also included to show that flow. This custom payment type includes everything just needs to be added
    to the store. 
    ![](GifExamples/AliPay.gif)
