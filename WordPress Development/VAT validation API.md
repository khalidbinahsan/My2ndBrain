```JS
$("#rm-form-next-btn").on("click", function(e){
        jQuery(document).ready(function ($) {
  $("#input_id_Textbox_71").on("input", function (e) {
    let vatField = $("#input_id_Textbox_71");
    let vatNumber = vatField.val().trim();
    let errorField = $("#rmform-textbox_71-error");
    let nextBtn = $("#rm-form-next-btn");
    // Function to disable the button visually
    vatField.after(
      '<span id="vat-success-msg" style="color: green; margin-left: 10px;">✔ Valid VAT</span>'
    );
    let successMsg = $("#vat-success-msg");
    successMsg.hide();
    function disableButton() {
      nextBtn.prop("disabled", true).css({
        "pointer-events": "none",
        cursor: "not-allowed",
        "background-color": "#d9534f", // Red color for disabled state
        opacity: "0.6", // Reduce opacity to show it's inactive
      });
      successMsg.hide();
    }

    // Function to enable the button
    function enableButton() {
      nextBtn.prop("disabled", false).css({
        "pointer-events": "auto",
        cursor: "pointer",
        "background-color": "", // Restore original color
        opacity: "1",
      });
      successMsg.show();
    }
    errorField.text("VAT number is not valid").show();
    disableButton();
    // Only validate if the VAT number field is not empty
    if (vatNumber !== "" && vatNumber.length > 9) {
      e.preventDefault(); // Prevent moving to the next step initially

      // Make an API call to validate VAT
      $.ajax({
        url: `https://api.vatcomply.com/vat?vat_number=${vatNumber}`,
        type: "GET",
        dataType: "json",
        success: function (response) {
          if (response.valid) {
            errorField.text(""); // Clear error message
            vatField.removeClass("rm-form-field-error");
            console.log("success");
            enableButton();
          } else {
            errorField
              .text("Invalid VAT number. Please enter a valid VAT number.")
              .show();
            disableButton();
            console.log("false");
          }
        },
        error: function () {
          errorField
            .text("Error validating VAT. Please try again later.")
            .show();
          disableButton();
        },
      });
    }
  });
});
```