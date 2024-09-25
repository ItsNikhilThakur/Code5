* {
    box-sizing: border-box;
    font-family: 'Times New Roman', Times, serif; /* Set Times New Roman globally */
}

body {
    background: linear-gradient(135deg, #2eddff, #0467fb); /* Vibrant gradient background */
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: auto; /* Allow the body to grow with content */
    padding: 20px; /* Add some padding */
}

.container {
    height: auto; /* Allow the container to grow with content */
    padding: 20px;
    max-width: 1200px; /* Set a maximum width */
    margin: 0 auto; /* Center the container */
    background-color: #dcf9ff; /* Container background */
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    overflow-x: auto;
}


header {
    text-align: center;
}

h1 {
    font-size: 24px;
    margin-bottom: 10px;
    color: #333; /* Header color */
}

p {
    font-size: 14px;
    color: #666;
    margin-bottom: 20px;
}

.form-input {
    margin-bottom: 15px;
}

.form-input label {
    display: block;
    margin-bottom: 5px;
    font-size: 14px;
    color: #333; /* Label color */
}

.form-input-size {
    width: 100%; /* Full width for inputs */
    padding: 10px; /* Increased padding */
    font-size: 14px;
    border: 1px solid #ccc;
    border-radius: 4px;
    transition: border-color 0.3s; /* Smooth transition for focus */
}

.form-input-size:focus {
    border-color: #ff7e5f; /* Focus border color */
    outline: none; /* Remove default outline */
}

.error {
    font-size: 12px;
    color: red;
    margin-top: 5px;
}

button {
    width: 100%; /* Full width for buttons */
    padding: 10px;
    background-color: #28a745; /* Submit button color */
    color: #fff;
    border: none;
    border-radius: 4px;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 0.3s; /* Smooth transition for hover */
}

button:disabled {
    background-color: grey; /* Grey out the button when disabled */
    cursor: not-allowed; /* Not allowed cursor */
}

button:hover:not(:disabled) {
    background-color: #218838; /* Darker green on hover */
}

button.updateDelete {
    background-color: #007bff; /* Update/Delete button color */
    margin-top: 10px;
}

button.updateDelete:hover {
    background-color: #0056b3; /* Darker blue on hover */
}

/* Responsive Styles */
@media (max-width: 414px) {
    .container {
        margin: 0 1rem; /* Smaller margin for smaller screens */
        padding: 1rem; /* Adjust padding */
        width: 100%; /* Full width for smaller screens */
    }

    form {
        width: 100%; /* Full form width */
    }

    .form-input-size {
        height: 2rem; /* Decrease height on smaller screens */
    }

    button {
        width: 100%; /* Make buttons take up full width */
    }
}
//////////////////////////////////////////////////////////////////////////////////////////////////
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CRUD Operations</title>
    <style>
        * {
            box-sizing: border-box;
            font-family: 'Times New Roman', Times, serif; /* Set Times New Roman globally */
        }

        body {
            background: linear-gradient(135deg, #2eddff, #0467fb); /* Vibrant gradient background */
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .container {
            max-width: 600px; /* Adjust maximum width for better readability */
            width: 100%; /* Full width for smaller screens */
            margin: 0 auto; /* Center the container */
            padding: 40px 20px; /* Padding */
            background-color: #dcf9ff; /* Container background */
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        header {
            text-align: center;
        }

        h1 {
            font-size: 24px;
            margin-bottom: 10px;
            color: #333; /* Header color */
        }

        p {
            font-size: 14px;
            color: #666;
            margin-bottom: 20px;
        }

        .form-input {
            margin-bottom: 15px;
        }

        .form-input label {
            display: block;
            margin-bottom: 5px;
            font-size: 14px;
            color: #333; /* Label color */
        }

        .form-input-size {
            width: 100%; /* Full width for inputs */
            padding: 10px; /* Increased padding */
            font-size: 14px;
            border: 1px solid #ccc;
            border-radius: 4px;
            transition: border-color 0.3s; /* Smooth transition for focus */
        }

        .form-input-size:focus {
            border-color: #ff7e5f; /* Focus border color */
            outline: none; /* Remove default outline */
        }

        .error {
            font-size: 12px;
            color: red;
            margin-top: 5px;
        }

        button {
            width: 100%; /* Full width for buttons */
            padding: 10px;
            background-color: #28a745; /* Submit button color */
            color: #fff;
            border: none;
            border-radius: 4px;
            font-size: 16px;
            cursor: pointer;
            transition: background-color 0.3s; /* Smooth transition for hover */
        }

        button:disabled {
            background-color: grey; /* Grey out the button when disabled */
            cursor: not-allowed; /* Not allowed cursor */
        }

        button:hover:not(:disabled) {
            background-color: #218838; /* Darker green on hover */
        }

        button.updateDelete {
            background-color: #007bff; /* Update/Delete button color */
            margin-top: 10px;
        }

        button.updateDelete:hover {
            background-color: #0056b3; /* Darker blue on hover */
        }

        /* Responsive Styles */
        @media (max-width: 414px) {
            .container {
                padding: 20px; /* Adjust padding */
            }

            .form-input-size {
                height: 2rem; /* Decrease height on smaller screens */
            }
        }
    </style>
</head>

<body>
    <div class="container">
        <header>
            <h1>Submit Your Details</h1>
        </header>

        <form id="userForm">
            <div class="form-input">
                <label for="firstname">First Name</label>
                <input type="text" id="firstname" name="firstname" placeholder="First Name" class="form-input-size" required autocomplete="given-name">
                <div class="error" id="firstnameError"></div>
            </div>

            <div class="form-input">
                <label for="lastname">Last Name</label>
                <input type="text" id="lastname" name="lastname" placeholder="Last Name" class="form-input-size" required autocomplete="family-name">
                <div class="error" id="lastnameError"></div>
            </div>

            <div class="form-input">
                <label for="email">Email Address</label>
                <input type="email" id="email" name="email" placeholder="Email Address" class="form-input-size" required autocomplete="email">
                <div class="error" id="emailError"></div>
            </div>

            <div class="form-input">
                <label for="countrycode">Country Code</label>
                <select id="countrycode" name="countrycode" class="form-input-size" required>
                    <option value="">Select Country Code</option>
                    <option value="+1">USA (+1)</option>
                    <option value="+91">India (+91)</option>
                    <option value="+44">UK (+44)</option>
                </select>
                <div class="error" id="countrycodeError"></div>
            </div>

            <div class="form-input">
                <label for="mobileno">Mobile No.</label>
                <input type="text" id="mobileno" name="mobileno" placeholder="Mobile No." class="form-input-size" required autocomplete="tel">
                <div class="error" id="mobilenoError"></div>
            </div>

            <div class="form-input terms-container">
                <label>
                <input type="checkbox" id="terms" name="terms"> I agree to the Terms & Conditions
                </label>
            </div>

            <div class="form-input">
                <button type="submit" class="submit" disabled id="submit">Submit Record</button>
                <button type="button" class="updateDelete">Update/Delete</button>
            </div>
        </form>

        <div id="responseMessage"></div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
    <script>
        $(document).ready(function() {
            function validateForm() {
                const firstname = $('#firstname').val();
                const lastname = $('#lastname').val();
                const email = $('#email').val();
                const countrycode = $('#countrycode').val();
                const mobileno = $('#mobileno').val();
                const isTermsChecked = $('#terms').is(':checked');
                const emailValid = /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
                const mobileValid = /^\d{10}$/.test(mobileno);

                // Reset error messages
                $(".error").text("");

                let isValid = true;

                if (!firstname) {
                    $("#firstnameError").text("* This field is required.");
                    isValid = false;
                }

                if (!lastname) {
                    $("#lastnameError").text("* This field is required.");
                    isValid = false;
                }

                if (!emailValid) {
                    $("#emailError").text("* Please enter a valid email address.");
                    isValid = false;
                }

                if (!countrycode) {
                    $("#countrycodeError").text("* Please select a country code.");
                    isValid = false;
                }

                if (!mobileValid) {
                    $("#mobilenoError").text("* Mobile number must contain exactly 10 digits.");
                    isValid = false;
                }

                if (!isTermsChecked) {
                    $("#mobilenoError").append("<br>* You must agree to the terms.");
                    isValid = false;
                }

                $("#submit").prop("disabled", !isValid);
            }

            // Enable/disable submit button based on form validity
            $("input, select").on("input change", validateForm);
            $("#terms").on("change", validateForm);

            $("#userForm").on("submit", function(event) {
                event.preventDefault();

                const firstname = $('#firstname').val();
                const lastname = $('#lastname').val();
                const email = $('#email').val();
                const countrycode = $('#countrycode').val();
                const mobileno = $('#mobileno').val();

                $.ajax({
                    type: "POST",
                    url: "https://mcsz6740-shssv34d-jxn10f-nm8.pub.sfmc-content.com/jn4ta43fo1r",
                    crossDomain: true,
                    dataType: 'text',
                    data: {
                        firstname: firstname,
                        lastname: lastname,
                        email: email,
                        countrycode: countrycode,
                        mobileno: mobileno
                    },
                    success: function(data) {
                        $("#responseMessage").html("<p>Record inserted successfully!</p>");
                        setTimeout(function() {
                            location.reload(); // Refresh the page after 3 seconds
                        }, 3000);
                    },
                    error: function(jqXHR, textStatus, errorThrown) {
                        $("#responseMessage").html("<p>Error: " + jqXHR.responseText + "</p>");
                    }
                });
            });

            $(".updateDelete").on("click", function () {
                window.location.href = "newform2.html"; // Update this URL as needed
            });
        });
    </script>
</body>
</html>
////////////////////////////////////////////////////////////////////////////////////////
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fetch Records</title>
    <link rel="stylesheet" href="style.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
    <style>
        * {
            box-sizing: border-box;
            font-family: 'Times New Roman', Times, serif; /* Global font */
        }

        body {
            background: linear-gradient(135deg, #2eddff, #0467fb); /* Vibrant gradient background */
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: auto; /* Allow the body to grow with content */
            padding: 20px; /* Add some padding */
        }

        .container {
            height: auto; /* Allow the container to grow with content */
            padding: 20px;
            max-width: 1200px; /* Set a maximum width */
            margin: 0 auto; /* Center the container */
            background-color: #dcf9ff; /* Container background */
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            overflow-x: auto;
            position: relative; /* Position relative for absolute positioning of the home link */
        }

        h1 {
            text-align: center;
            color: #333;
        }

        .search-bar {
            margin-bottom: 20px;
            text-align: center;
        }

        .search-bar input {
            padding: 10px;
            width: 80%; /* Width of the search input */
            max-width: 400px; /* Max width for larger screens */
            border: 1px solid #ccc;
            border-radius: 4px;
        }

        table {
            width: 100%; /* Full width */
            border-collapse: collapse; /* Merge table borders */
        }

        th, td {
            border: 1px solid #ddd; /* Add border to cells */
            padding: 8px; /* Cell padding */
            text-align: left; /* Align text to the left */
        }

        th {
            background-color: #f2f2f2; /* Header background color */
        }

        /* Home link style */
        .home-link {
            position: absolute;
            top: 20px;
            left: 20px;
            text-decoration: none;
            color: #007bff; /* Link color */
            font-size: 14px; /* Font size */
        }

        .home-link:hover {
            text-decoration: underline; /* Underline on hover */
        }

        /* Responsive design */
        @media (max-width: 600px) {
            table, thead, tbody, th, td, tr {
                display: block; /* Stack elements */
            }
            thead tr {
                position: absolute; /* Position header above content */
                top: -9999px; /* Hide it off-screen */
                left: -9999px; /* Hide it off-screen */
            }
            tr {
                margin: 0 0 1rem 0; /* Space between rows */
            }
            td {
                text-align: right; /* Align text to the right */
                padding-left: 50%; /* Space for labels */
                position: relative; /* Position for pseudo-elements */
            }
            td::before {
                content: attr(data-label); /* Use data-label for mobile */
                position: absolute; /* Position labels */
                left: 0;
                width: 50%; /* Space for labels */
                padding-left: 10px; /* Label padding */
                text-align: left; /* Align labels to the left */
                font-weight: bold; /* Bold labels */
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <a href="file:///C:/Users/Nikhil.Thakur04/Documents/Code/newform.html" class="home-link">Home</a>
        <h1>Fetched Records</h1>

        <div class="search-bar">
            <input type="text" id="searchInput" placeholder="Search Records...">
        </div>

        <table id="recordsTable">
            <thead>
                <tr>
                    <th>First Name</th>
                    <th>Last Name</th>
                    <th>Email</th>
                    <th>Country Code</th>
                    <th>Mobile No.</th>
                    <th>Actions</th>
                </tr>
            </thead>
            <tbody>
                <!-- Fetched records will be appended here -->
            </tbody>
        </table>
    </div>

    <script>
        function fetchRecords() {
            $.ajax({
                type: "GET",
                url: "https://mcsz6740-shssv34d-jxn10f-nm8.pub.sfmc-content.com/fa4pew2hg1n",
                crossDomain: true,
                dataType: 'text',
                success: function (data) {
                    const tbody = $("#recordsTable tbody");
                    tbody.empty(); // Clear existing records

                    const totalCount = parseInt(data.split('totalCount={').pop().split('}')[0], 10);

                    if (totalCount > 0) {
                        for (let i = 1; i <= totalCount; i++) {
                            const firstname = data.split(`firstname${i}={`).pop().split('}')[0];
                            const lastname = data.split(`lastname${i}={`).pop().split('}')[0];
                            const email = data.split(`email${i}={`).pop().split('}')[0];
                            const countrycode = data.split(`countrycode${i}={`).pop().split('}')[0];
                            const mobileno = data.split(`mobileno${i}={`).pop().split('}')[0];

                            tbody.append(`
                                <tr>
                                    <td data-label="First Name">${firstname}</td>
                                    <td data-label="Last Name">${lastname}</td>
                                    <td data-label="Email">${email}</td>
                                    <td data-label="Country Code">${countrycode}</td>
                                    <td data-label="Mobile No.">${mobileno}</td>
                                    <td data-label="Actions">
                                        <button style="color: white; background-color: red;" class="delete" data-id="${email}">Delete</button> 
                                        <button class="update" data-record='${JSON.stringify({firstname, lastname, email, countrycode, mobileno})}'>Update</button>
                                    </td>
                                </tr>
                            `);
                        }
                    } else {
                        tbody.append("<tr><td colspan='6'>No records found.</td></tr>");
                    }
                },
                error: function (jqXHR, textStatus, errorThrown) {
                    $("#recordsTable tbody").html(`<tr><td colspan='6'>Error fetching records: ${textStatus} - ${errorThrown}</td></tr>`);
                }
            });
        }

        $(document).ready(function() {
            fetchRecords();

            // Search functionality
            $("#searchInput").on("keyup", function() {
                const value = $(this).val().toLowerCase();
                $("#recordsTable tbody tr").filter(function() {
                    $(this).toggle($(this).text().toLowerCase().indexOf(value) > -1);
                });
            });

            $(document).on("click", ".delete", function() {
                const id = $(this).data("id");
                $.ajax({
                    type: "POST",
                    url: "https://mcsz6740-shssv34d-jxn10f-nm8.pub.sfmc-content.com/p4ci0uooeed",
                    crossDomain: true,
                    dataType: 'text',
                    data: { email: id },
                    success: function() {
                        setTimeout(fetchRecords, 100); // Refresh records after 0.1 second
                    },
                    error: function() {
                        alert("Error deleting record.");
                    }
                });
            });

            $(document).on("click", ".update", function() {
                const record = $(this).data("record");
                updateRecord(record);
            });
        });

        function updateRecord(record) {
            const { firstname, lastname, email, countrycode, mobileno } = record;
            const url = `file:///C:/Users/Nikhil.Thakur04/Documents/Code/newform3.html?firstname=${encodeURIComponent(firstname)}&lastname=${encodeURIComponent(lastname)}&email=${encodeURIComponent(email)}&countrycode=${encodeURIComponent(countrycode)}&mobileno=${encodeURIComponent(mobileno)}`;
            window.location.href = url;
        }
    </script>
</body>
</html>
////////////////////////////////////////////////////////////////////////////////
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="style.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
    <title>Update Your Details</title>
    <style>
        * {
            box-sizing: border-box;
            font-family: 'Times New Roman', Times, serif; /* Global font */
        }

        body {
            background: linear-gradient(135deg, #2eddff, #0467fb); /* Vibrant gradient background */
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: auto; /* Allow the body to grow with content */
            padding: 20px; /* Add some padding */
        }

        .container {
            height: auto; /* Allow the container to grow with content */
            padding: 20px;
            max-width: 600px; /* Set a maximum width */
            margin: 0 auto; /* Center the container */
            background-color: #dcf9ff; /* Container background */
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            position: relative; /* Position relative for absolute positioning of links */
        }

        h1 {
            text-align: center;
            color: #333;
        }

        /* Home and Fetch Records link styles */
        .home-link, .fetch-records-link {
            position: absolute;
            top: 20px;
            text-decoration: none;
            color: #007bff; /* Link color */
            font-size: 14px; /* Font size */
        }

        .home-link {
            left: 20px; /* Position for Home link */
        }

        .fetch-records-link {
            right: 20px; /* Position for Fetch Records link */
        }

        .home-link:hover, .fetch-records-link:hover {
            text-decoration: underline; /* Underline on hover */
        }

        /* Form input styles */
        .form-input {
            margin-bottom: 15px;
        }

        .form-input-size {
            width: 100%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }

        .error {
            color: red;
            font-size: 12px;
        }

        .submit {
            background-color: #007bff;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 4px;
            cursor: pointer;
        }

        .submit:disabled {
            background-color: #ccc; /* Disable button style */
        }
    </style>
</head>
<body>
    <div class="container">
        <a href="file:///C:/Users/Nikhil.Thakur04/Documents/Code/newform.html" class="home-link">Home</a>
        <a href="file:///C:/Users/Nikhil.Thakur04/Documents/Code/newform2.html" class="fetch-records-link">Fetch Records</a>
        <header>
            <h1>Update Your Details</h1>
            <p>Please fill in the form below to update your details.</p>
        </header>
        <form id="updateForm">
            <div class="form-input">
                <label for="firstname">First Name</label>
                <input type="text" id="firstname" name="firstname" placeholder="First Name" required class="form-input-size">
                <div class="error" id="firstnameError"></div>
            </div>

            <div class="form-input">
                <label for="lastname">Last Name</label>
                <input type="text" id="lastname" name="lastname" placeholder="Last Name" required class="form-input-size">
                <div class="error" id="lastnameError"></div>
            </div>

            <div class="form-input">
                <label for="email">Email Address</label>
                <input type="email" id="email" name="email" placeholder="Email Address" required disabled class="form-input-size">
                <div class="error" id="emailError"></div>
            </div>

            <div class="form-input">
                <label for="countrycode">Country Code</label>
                <select id="countrycode" name="countrycode" required class="form-input-size">
                    <option value="">Select Country Code</option>
                    <option value="+1">USA (+1)</option>
                    <option value="+91">India (+91)</option>
                    <option value="+44">UK (+44)</option>
                </select>
                <div class="error" id="countrycodeError"></div>
            </div>

            <div class="form-input">
                <label for="mobileno">Mobile No.</label>
                <input type="text" id="mobileno" name="mobileno" placeholder="Mobile No." required class="form-input-size">
                <div class="error" id="mobilenoError"></div>
            </div>

            <div class="form-input">
                <label>
                    <input type="checkbox" id="terms" name="terms"> I agree to the Terms & Conditions
                </label>
                <div class="error" id="termsError"></div>
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
            if (email) $('#email').val(email);
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

                // Clear previous error messages
                $(".error").text("");

                // Simple validation checks
                if (!firstname) {
                    $("#firstnameError").text("* This field is required.");
                    isValid = false;
                }

                if (!lastname) {
                    $("#lastnameError").text("* This field is required.");
                    isValid = false;
                }

                const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
                if (!email || !emailRegex.test(email)) {
                    $("#emailError").text("* Please enter a valid email address.");
                    isValid = false;
                }

                if (!countrycode) {
                    $("#countrycodeError").text("* Please select a country code.");
                    isValid = false;
                }

                if (!/^\d{10}$/.test(mobileno)) {
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
                    email: $('#email').val(),
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
                         setTimeout(function() {
                        window.location.href = "file:///C:/Users/Nikhil.Thakur04/Documents/Code/newform.html";
                    }, 3000); // 3000 milliseconds = 3 seconds
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
