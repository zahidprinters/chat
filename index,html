<?php
session_start();

// Define users and their passwords (hardcoded for simplicity)
$users = [
    'user1' => 'password1',
    'user2' => 'password2'
];

// Handle login
if ($_SERVER['REQUEST_METHOD'] === 'POST' && isset($_POST['username'], $_POST['password'])) {
    $username = htmlspecialchars($_POST['username']);
    $password = $_POST['password'];

    if (isset($users[$username]) && $users[$username] === $password) {
        $_SESSION['username'] = $username;
    } else {
        $error = "Invalid username or password.";
    }
}

// Handle logout
if (isset($_GET['logout'])) {
    session_unset();
    session_destroy();
    header('Location: index.php');
    exit;
}

// Handle message submission
if ($_SERVER['REQUEST_METHOD'] === 'POST' && isset($_POST['message']) && isset($_SESSION['username'])) {
    $message = htmlspecialchars($_POST['message']);
    $username = $_SESSION['username'];
    
    if (!empty($message)) {
        file_put_contents('messages.txt', "$username: $message\n", FILE_APPEND);
    }
    header('Location: index.php');
    exit;
}
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Chat</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f1f1f1;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            color: #333;
        }

        .chat-container {
            width: 450px;
            background: #ffffff;
            border-radius: 8px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            padding: 20px;
            transition: transform 0.3s ease;
        }

        .chat-container:hover {
            transform: scale(1.02);
        }

        h1 {
            text-align: center;
            color: #007BFF;
            margin-bottom: 20px;
        }

        .messages {
            height: 350px;
            overflow-y: auto;
            padding: 10px;
            margin-bottom: 15px;
            background: #f9f9f9;
            border-radius: 6px;
            border: 1px solid #ddd;
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .message {
            padding: 12px;
            border-radius: 8px;
            word-wrap: break-word;
            box-sizing: border-box;
            font-size: 16px;
            max-width: 85%;
            display: inline-block;
        }

        .message.other {
            background: #e6e6e6;
            color: #333;
            align-self: flex-start;
            text-align: left;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }

        .message.user {
            background: #007BFF;
            color: white;
            align-self: flex-end;
            text-align: right;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }

        .username {
            font-weight: bold;
            color: #007BFF;
            margin-bottom: 5px;
        }

        form {
            display: flex;
            flex-direction: column;
        }

        input[type="text"], input[type="password"], input[type="text"][name="message"] {
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 6px;
            margin-bottom: 15px;
            font-size: 16px;
            transition: border-color 0.3s ease;
        }

        input[type="text"]:focus, input[type="password"]:focus, input[type="text"][name="message"]:focus {
            border-color: #007BFF;
            outline: none;
        }

        button {
            padding: 12px;
            background-color: #007BFF;
            color: white;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 16px;
            transition: background-color 0.3s ease;
        }

        button:hover {
            background-color: #0056b3;
        }

        .logout-button {
            padding: 12px;
            background-color: #FF5733;
            color: white;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 16px;
            margin-top: 20px;
            width: 100%;
        }

        .logout-button:hover {
            background-color: #c0392b;
        }

        .error {
            color: red;
            text-align: center;
            margin-bottom: 15px;
            font-size: 14px;
        }
    </style>
</head>
<body>
    <div class="chat-container">
        <?php if (!isset($_SESSION['username'])): ?>
            <h1>Login</h1>
            <?php if (isset($error)) echo "<div class='error'>$error</div>"; ?>
            <form method="POST">
                <input type="text" name="username" placeholder="Username" required>
                <input type="password" name="password" placeholder="Password" required>
                <button type="submit">Login</button>
            </form>
        <?php else: ?>
            <h1>Welcome, <?php echo htmlspecialchars($_SESSION['username']); ?>!</h1>
            <div class="messages">
                <?php
                // Display the last 10 chat messages from the file
                if (file_exists('messages.txt')) {
                    $messages = array_reverse(file('messages.txt', FILE_IGNORE_NEW_LINES));
                    $messages = array_slice($messages, 0, 10); // Show only the last 10 messages

                    foreach ($messages as $message) {
                        // Split message into username and message content
                        $messageParts = explode(':', $message, 2);
                        $username = trim($messageParts[0]);
                        $messageText = htmlspecialchars($messageParts[1]);

                        // Assign CSS class based on the user
                        $class = ($username === $_SESSION['username']) ? 'user' : 'other';
                        echo "<div class='message $class'><span class='username'>$username:</span> $messageText</div>";
                    }
                }
                ?>
            </div>
            <form method="POST">
                <input type="text" name="message" placeholder="Type your message..." required>
                <button type="submit">Send</button>
            </form>
            <a href="index.php?logout=true"><button class="logout-button">Logout</button></a>
        <?php endif; ?>
    </div>
</body>
</html>
