# Code5
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="style.css"> <!-- Link to the same CSS file -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
    <title>Update Your Details</title>
</head>
<body>
    <div class="container">
        <header>
            <h1>Update Your Details</h1>
            <p>Please fill in the form below to update your details.</p>
        </header>
        <form id="updateForm">
            <div class="form-input">
                <label for="firstname">First Name</label>
                <input type="text" id="firstname" name="firstname" placeholder="First Name" required class="form-input-size">
                <div class="error" id="firstnameError"></div> <!-- Error message for First Name -->
            </div>

            <div class="form-input">
                <label for="lastname">Last Name</label>
                <input type="text" id="lastname" name="lastname" placeholder="Last Name" required class="form-input-size">
                <div class="error" id="lastnameError"></div> <!-- Error message for Last Name -->
            </div>

            <div class="form-input">
                <label for="email">Email Address</label>
                <input type="email" id="email" name="email" placeholder="Email Address" required disabled class="form-input-size">
                <div class="error" id="emailError"></div> <!-- Error message for Email -->
            </div>

            <div class="form-input">
                <label for="countrycode">Country Code</label>
                <select id="countrycode" name="countrycode" required class="form-input-size">
                    <option value="">Select Country Code</option>
                    <option value="+1">USA (+1)</option>
                    <option value="+91">India (+91)</option>
                    <option value="+44">UK (+44)</option>
                </select>
                <div class="error" id="countrycodeError"></div> <!-- Error message for Country Code -->
            </div>

            <div class="form-input">
                <label for="mobileno">Mobile No.</label>
                <input type="text" id="mobileno" name="mobileno" placeholder="Mobile No." required class="form-input-size">
                <div class="error" id="mobilenoError"></div> <!-- Error message for Mobile No -->
            </div>

            <div class="form-input">
                <label>
                    <input type="checkbox" id="terms" name="terms"> I agree to the Terms & Conditions
                </label>
                <div class="error" id="termsError"></div> <!-- Error message for Terms -->
            </div>

            <div class="form-input">
                <button type="submit" id="submit" class="submit" disabled>Update Record</button>
            </div>
        </form>
        <div id="responseMessage"></div>
    </div>

    <script>
        $(document).ready(function() {
            const urlParams = new URLSearchParams(window.location.search);

            // Extract values from URL parameters
            const firstname = urlParams.get('firstname');
            const lastname = urlParams.get('lastname');
            const email = urlParams.get('email');
            const countrycode = urlParams.get('countrycode');
            const mobileno = urlParams.get('mobileno');

            // Pre-fill the form fields if values are present
            if (firstname) $('#firstname').val(firstname);
            if (lastname) $('#lastname').val(lastname);
            if (email) $('#email').val(email); // Email will be displayed but not editable
            if (countrycode) $('#countrycode').val(countrycode);
            if (mobileno) $('#mobileno').val(mobileno);

            // Form validation function
            function validateForm() {
                let isValid = true;
                const firstname = $('#firstname').val();
                const lastname = $('#lastname').val();
                const email = $('#email').val();
                const countrycode = $('#countrycode').val();
                const mobileno = $('#mobileno').val();
                const isTermsChecked = $('#terms').is(":checked");

                // Simple validation checks
                if (!firstname) {
                    $("#firstnameError").text("* This field is required.");
                    isValid = false;
                }

                if (!lastname) {
                    $("#lastnameError").text("* This field is required.");
                    isValid = false;
                }

                if (!email) {
                    $("#emailError").text("* Please enter a valid email address.");
                    isValid = false;
                }

                if (!countrycode) {
                    $("#countrycodeError").text("* Please select a country code.");
                    isValid = false;
                }

                if (mobileno.length !== 10) {
                    $("#mobilenoError").text("* Mobile number must contain exactly 10 digits.");
                    isValid = false;
                }

                if (!isTermsChecked) {
                    $("#termsError").text("* You must agree to the terms.");
                    isValid = false;
                }

                $("#submit").prop("disabled", !isValid);
            }

            // Enable/disable submit button based on form validity
            $("input, select").on("input change", validateForm);
            $("#terms").on("change", validateForm);

            $("#updateForm").on("submit", function(event) {
                event.preventDefault();

                const updatedData = {
                    firstname: $('#firstname').val(),
                    lastname: $('#lastname').val(),
                    email: $('#email').val(), // Email will be sent but not updated
                    countrycode: $('#countrycode').val(),
                    mobileno: $('#mobileno').val()
                };

                // AJAX call to submit the updated data
                $.ajax({
                    type: "POST",
                    url: "https://mcsz6740-shssv34d-jxn10f-nm8.pub.sfmc-content.com/sioy3rl2fa2",
                    data: updatedData,
                    crossDomain: true,
                    dataType: 'text',
                    success: function(response) {
                        $("#responseMessage").html("<p>Record updated successfully!</p>");
                    },
                    error: function(jqXHR, textStatus, errorThrown) {
                        $("#responseMessage").html("<p>Error: " + textStatus + " - " + errorThrown + "</p>");
                    }
                });
            });
        });
    </script>
</body>
</html>
