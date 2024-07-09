<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Investment Return Calculator</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>
    <h1>Investment Return Calculator</h1>
    <form id="investment-form">
        <label for="total-investment">Total Investment:</label>
        <input type="number" id="total-investment" name="total_investment" required>
        <br>
        <label for="group-a-investment">Group A Investment:</label>
        <input type="number" id="group-a-investment" name="group_a_investment" required>
        <label for="group-a-return">Group A Return (%):</label>
        <input type="number" id="group-a-return" name="group_a_return" required>
        <br>
        <label for="group-b-investment">Group B Investment:</label>
        <input type="number" id="group-b-investment" name="group_b_investment" required>
        <label for="group-b-return">Group B Return (%):</label>
        <input type="number" id="group-b-return" name="group_b_return" required>
        <br>
        <label for="group-c-investment">Group C Investment:</label>
        <input type="number" id="group-c-investment" name="group_c_investment" required>
        <label for="group-c-return">Group C Return (%):</label>
        <input type="number" id="group-c-return" name="group_c_return" required>
        <br>
        <button type="submit">Calculate</button>
    </form>
    <div id="results"></div>
    <script>
        const backendUrl = 'https://<your-render-backend-url>'; // Replace with your Render backend URL

        $('#investment-form').on('submit', function(event) {
            event.preventDefault();
            $.ajax({
                url: `${backendUrl}/calculate`,
                method: 'POST',
                contentType: 'application/json',
                data: JSON.stringify({
                    total_investment: $('#total-investment').val(),
                    group_a_investment: $('#group-a-investment').val(),
                    group_a_return: $('#group-a-return').val(),
                    group_b_investment: $('#group-b-investment').val(),
                    group_b_return: $('#group-b-return').val(),
                    group_c_investment: $('#group-c-investment').val(),
                    group_c_return: $('#group-c-return').val()
                }),
                success: function(response) {
                    $('#results').html('<pre>' + JSON.stringify(response, null, 2) + '</pre>');
                }
            });
        });
    </script>
</body>
</html>
