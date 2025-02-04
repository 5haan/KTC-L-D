
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LMS App</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" integrity="sha512-8tY3b3tshtDYpiDoVGG/kAEVdri5zqJiTLyTV20ZTNQjE1eVpnN5+o4SIAfI6CZJdFQ3FQOtXSPyrQ8MWy5g==" crossorigin="anonymous" referrerpolicy="no-referrer" />
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
        }
        .container {
            max-width: 1200px;
            margin: 40px auto;
            padding: 20px;
            background-color: #f9f9f9;
            border: 1px solid #ddd;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        .modal-dialog {
            max-width: 400px;
        }
    </style>
</head>
<body>
    <div class="container">
        <nav class="navbar navbar-expand-lg navbar-light bg-light">
            <div class="container-fluid">
                <a class="navbar-brand" href="#">LMS App</a>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse" id="navbarSupportedContent">
                    <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                        <li class="nav-item">
                            <a class="nav-link active" aria-current="page" href="#">Home</a>
                        </li>
                        <li class="nav-item">
                            <a class="nav-link" href="#">Login</a>
                        </li>
                        <li class="nav-item">
                            <a class="nav-link" href="#">Admin</a>
                        </li>
                    </ul>
                </div>
            </div>
        </nav>
        <div class="row">
            <div class="col-md-6">
                <h2>Login</h2>
                <form id="login-form">
                    <div class="mb-3">
                        <label for="mobile-number" class="form-label">Mobile Number</label>
                        <input type="text" class="form-control" id="mobile-number" placeholder="Enter mobile number">
                    </div>
                    <button type="submit" class="btn btn-primary">Send OTP</button>
                </form>
            </div>
            <div class="col-md-6">
                <h2>Admin</h2>
                <form id="admin-form">
                    <div class="mb-3">
                        <label for="content-type" class="form-label">Content Type</label>
                        <select class="form-select" id="content-type">
                            <option value="video">Video</option>
                            <option value="text">Text</option>
                            <option value="pdf">PDF</option>
                            <option value="ppt">PPT</option>
                        </select>
                    </div>
                    <div class="mb-3">
                        <label for="content" class="form-label">Content</label>
                        <input type="file" class="form-control" id="content">
                    </div>
                    <button type="submit" class="btn btn-primary">Upload Content</button>
                </form>
            </div>
        </div>
        <div class="row">
            <div class="col-md-12">
                <h2>Lesson Wise Content</h2>
                <div id="lesson-content"></div>
            </div>
        </div>
    </div>
    <div class="modal fade" id="otp-modal" tabindex="-1" aria-labelledby="otp-modal-label" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="otp-modal-label">OTP Verification</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <form id="otp-form">
                        <div class="mb-3">
                            <label for="otp" class="form-label">Enter OTP</label>
                            <input type="text" class="form-control" id="otp" placeholder="Enter OTP">
                        </div>
                        <button type="submit" class="btn btn-primary">Verify OTP</button>
                    </form>
                </div>
            </div>
        </div>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p" crossorigin="anonymous"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/js/all.min.js" integrity="sha512-AhcNPomR7h6sXzJJ1t+R5LcNG3Wfyd7r0mNt1u1q2JpqZxU9x0tHyyK0B4jLTo6NPRdLSAQobWf6c+8+sLjXg==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
    <script>
        const loginForm = document.getElementById('login-form');
        const adminForm = document.getElementById('admin-form');
        const otpForm = document.getElementById('otp-form');
        const lessonContent = document.getElementById('lesson-content');
        const otpModal = document.getElementById('otp-modal');
        const otpInput = document.getElementById('otp');
        const contentInput = document.getElementById('content');
        const contentTypeSelect = document.getElementById('content-type');
        let otp = '';
        let content = '';
        let contentType = '';
        loginForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const mobileNumber = document.getElementById('mobile-number').value;
            // send OTP to mobile number
            otp = Math.floor(100000 + Math.random() * 900000);
            console.log(otp);
            otpModal.modal('show');
        });
        otpForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const userOtp = otpInput.value;
            if (userOtp === otp.toString()) {
                // login successful
                console.log('Login successful');
                otpModal.modal('hide');
            } else {
                console.log('Invalid OTP');
            }
        });
        adminForm.addEventListener('submit', (e) => {
            e.preventDefault();
            content = contentInput.files[0];
            contentType = contentTypeSelect.value;
            // upload content to server
            console.log(content, contentType);
        });
        // generate lesson wise content
        const lessons = [
            { id: 1, title: 'Lesson 1', content: 'This is lesson 1 content' },
            { id: 2, title: 'Lesson 2', content: 'This is lesson 2 content' },
            { id: 3, title: 'Lesson 3', content: 'This is lesson 3 content' }
        ];
        lessons.forEach((lesson) => {
            const lessonHtml = `
                <h3>${lesson.title}</h3>
                <p>${lesson.content}</p>
                <button class="btn btn-primary">Assessment</button>
                <button class="btn btn-primary">Certificate</button>
            `;
            lessonContent.innerHTML += lessonHtml;
        });
    </script>
</body>
</html>
