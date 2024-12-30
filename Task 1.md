# Task 01

## Description

A very basic HTML webpage using all HTML tags

```bash
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
   
    <title>Radiohead Fan Page</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            color: #333;
            line-height: 1.6;
        }
        header {
            background: #222;
            color: #fff;
            padding: 10px 0;
            text-align: center;
        }
        nav {
            margin: 10px 0;
            text-align: center;
        }
        nav a {
            margin: 0 10px;
            text-decoration: none;
            color: #222;
        }
        footer {
            text-align: center;
            padding: 10px;
            background: #222;
            color: #fff;
            margin-top: 20px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
        }
        table, th, td {
            border: 1px solid #ccc;
        }
        th, td {
            padding: 10px;
            text-align: left;
        }
    </style>
</head>
<body>
    <header>
        <h1>Welcome to the Radiohead Fan Page</h1>
        <p>A tribute to the legendary band that redefined music.</p>
    </header>

    <nav>
        <a href="#about">About</a>
        <a href="#members">Band Members</a>
        <a href="#albums">Albums</a>
        <a href="#contact">Contact</a>
    </nav>

    <main>
        <section id="about">
            <h2>About Radiohead</h2>
            <p><strong>Radiohead</strong> Radiohead are a touchstone for all that is fearless and adventurous in rock, evolving from self-loathing anthems to moody prog rock suites to weathered, if shimmering ballads. Starting with their hit "Creep" from <em>Pablo Honey<em>, they progressed from alternative rock to experimental art-rock masterpieces like <em>OK Computer</em> and <em>Kid A</em>.</p>
            <blockquote>
                "This is what you get when you mess with us." - <cite>Karma Police</cite>
            </blockquote>
        </section>

        <section id="members">
            <h2>Band Members</h2>
            <ul>
                <li>Thom Yorke - Vocals, Guitar</li>
                <li>Jonny Greenwood - Guitar, Keyboards</li>
                <li>Ed O'Brien - Guitar, Backing Vocals</li>
                <li>Colin Greenwood - Bass</li>
                <li>Phil Selway - Drums</li>
            </ul>
        </section>

        <section id="albums">
            <h2>Top Albums</h2>
            <table>
                <thead>
                    <tr>
                        <th>Album</th>
                        <th>Release Year</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>Pablo Honey</td>
                        <td>1993</td>
                    </tr>
                    <tr>
                        <td>The Bends</td>
                        <td>1995</td>
                    </tr>
                    <tr>
                        <td>OK Computer</td>
                        <td>1997</td>
                    </tr>
                    <tr>
                        <td>Kid A</td>
                        <td>2000</td>
                    </tr>
                    <tr>
                        <td>In Rainbows</td>
                        <td>2007</td>
                    </tr>
                </tbody>
            </table>
        </section>

        <section id="contact">
            <h2>Contact Us</h2>
            <form action="#" method="post">
                <label for="name">Name:</label><br>
                <input type="text" id="name" name="name" required><br><br>

                <label for="email">Email:</label><br>
                <input type="email" id="email" name="email" required><br><br>

                <label for="message">Message:</label><br>
                <textarea id="message" name="message" rows="4" cols="50"></textarea><br><br>

                <button type="submit">Submit</button>
            </form>
        </section>
    </main>

    <footer>
        <p>&copy; 2024 Radiohead Fan Page. All Rights Reserved.</p>
    </footer>
</body>
</html>
```
