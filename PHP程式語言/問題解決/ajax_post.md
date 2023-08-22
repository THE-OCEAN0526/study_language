## 問題
login_process.php沒有post到資料，但是我再ajax寫console.log(data)有資料，login_process.php一直執行到"沒收到"
<img src="https://github.com/THE-OCEAN0526/Studyed-Program-Language/assets/122972916/ead0f6da-bcbe-43f9-9436-5754ca2f0452" width="300">
<img src="https://github.com/THE-OCEAN0526/Studyed-Program-Language/assets/122972916/929c9da4-b70d-41d8-9658-68ab7c2413d5" width="500">
<img src="https://github.com/THE-OCEAN0526/Studyed-Program-Language/assets/122972916/f9dbf4e7-7833-446d-a379-542d319d932d" width="500"><br>
原先我的dataType:寫new FormData($("#login-form")[0]) 但後來後一直執行到error:所以我就改成圖片這樣 會不會是這個原因導致沒有post到，可是我input裡有寫name啊!?<br>
<img src="https://github.com/THE-OCEAN0526/Studyed-Program-Language/assets/122972916/56ba5db2-d575-40dc-a075-1891f3cbcad2" alt="image" width="400">
```php
<?php
// header('Content-Type: text/html; charset=utf-8');
session_start();
require '../login-signup/config.php';

$response = array(
    'status' => 0,
    'message' => '沒收到'
);

$errorEmail = false;
$errorpasswd = false;

if(isset($_POST['email']) || isset($_POST['password'])) {

    $email = filter_var($_POST['email'], FILTER_VALIDATE_EMAIL);
    $password = filter_var($_POST['password'], FILTER_SANITIZE_FULL_SPECIAL_CHARS);


    if(!$email){
        $response['message'] = "請輸入信箱帳號";
        $errorEmail= true;
    }elseif(!$password){
        $response['message'] = "請輸入密碼";
        $errorpasswd = true;
    }else{

        $pdo = new PDO("mysql:host=localhost;dbname=Pjl_user_info", "root", "");
        $checkQuery = "SELECT * FROM users WHERE email = :email";
        $stmt = $pdo->prepare($checkQuery);
        $stmt->bindParam(':email', $email);
        $stmt->execute();

        if($stmt->rowcount() === 1){
            // 將用戶數據轉換為陣列
            $get_user = $stmt->fetch(PDO::FETCH_ASSOC);
            // 獲取哈希資料庫密碼
            // get_user['該欄位名稱'];
            $database_password = $get_user['password'];

            if(password_verify($password, $database_password)){
                $response['status'] = 1;
                $_SESSION['user-id-session'] = $get_user['id'];
            }else{
                $response['message'] = "電子郵件或密碼不正確";
            }
        }else{
            $response['message'] = "該帳號尚未註冊";
        }
    }

}


echo json_encode($response, JSON_UNESCAPED_UNICODE);

?>
```
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- icon CSS -->
    <link rel="stylesheet" href="https://unicons.iconscout.com/release/v4.0.8/css/line.css">
    <!-- link CSS -->
    <link rel="stylesheet" href="../../CSS/login-signup/login.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.7.0/jquery.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-cookie/1.4.1/jquery.cookie.min.js"></script>
    <title>登入帳號</title>

</head>
<body>

    <div class="main-container">

        <!-- 登入表單 -->
        <div id="main-login">
            <div class="main-contents">
                <h2 class="title">登入帳號</h2>
    
                <form action="#" id="login-form">

                <!-- 顯示訊息 -->  

                    <div class="form-message"></div>
                    
                    <div class="input-box">
                        <input id="login-user" class="user-id" type="text" name="email" required>
                        <i class="uil uil-envelope email"></i>
                        <label for="user-id">信箱帳號</label>
                    </div>
        
                    <div class="input-box">
                        <input id="login-password" class="user-password" type="password" name="password" required>
                        <i class="uil uil-lock passwd"></i>
                        <i class="uil uil-eye-slash pw_hide"></i>
                        <label for="user-password">密碼</label>
                    </div>
        
                    <div class="remember-forgot">
                        <label for="remember"><input type="checkbox" id="remember">
                        記住帳號</label>
                        <a href="#">忘記密碼?</a>
                    </div>
        
                    <div class="btn-login">
                        <button id="login-btn" class="btn" type="submit" name="login">登入</button>
                    </div>
    
                    <div class="switch-form">
                        <p>還沒有帳號?
                            <a id="register-link">立即註冊</a>
                        </p>
                    </div>
    
                </form>
            </div>
        </div>


        <!-- 註冊表單 -->

        <div id="main-signup">
            <div class="main-contents">
                <h2 class="title">註冊帳號</h2>

                <form action="#" id="register-form" >
                    
                    <!-- 顯示驗證訊息 -->

                    <div class="form-message"></div>
                     

                    <div class="main-user-info">
                        <div class="input-box">
                            <label for="fullname"><i class="uil uil-user"></i>用戶名</label>
                            <input id="fullname" name="fullname"
                            type="text" placeholder="輸入用戶名">
                        </div>
        
                        <div class="input-box">
                            <label for="user_type"><i class="uil uil-social-distancing"></i>類型</label>
                            <select name="user_type" id="">
                                <option value="user">訪客</option>
                                <option value="admin">使用者</option>
                            </select>
                        </div>
        
        
                        <div class="input-box">
                            <label for="user-id"><i class="uil uil-envelope email"></i>信箱帳號</label>
                            <input class="user-id" type="text" name="email"
                            placeholder="輸入電子郵件">
                        </div>
            
                        <div class="input-box pw">
                            <label for="user-password"> <i class="uil uil-lock passwd"></i>密碼</label>
                            <input class="user-password" type="password" name="password"
                            placeholder="輸入密碼">
                            <i class="uil uil-eye-slash pw_hide"></i>
                        </div>
        
                        <div class="input-box">
                            <label for="user-repassword"><i class="uil uil-lock passwd"></i>確認密碼</label>
                            <input id="user-repassword" type="password" name="repassword"
                            placeholder="再次輸入密碼">
                        </div>

                    </div> 
                    
        
                    <div class="btn-register">
                        <button class="btn" type="submit" name="register">註冊</button>
                    </div>

                    <div class="switch-form">
                        <p>已經有帳號?
                        <a href="#" id="login-link">立即登入</a>
                        </p>
                    </div>

                </form>
            </div>
        </div>
    </div>

    <!-- change form -->
    <script src="../../JS/login.js"></script>
    <!-- ajax message -->
    <script src="../../JS/ajaxform.js"></script>
    <!-- jquery link -->
    <!-- <script src="../../JS/jquery.min.js"></script> -->
    
</body>
</html>
```

## 解決辦法
你試著把POST的資料存到response確認一下資料傳遞是否OK
```php
<?php
// header('Content-Type: text/html; charset=utf-8');
session_start();
require '../login-signup/config.php';

$response = array(
    'status' => 0,
    'message' => '沒收到',
    'receivedEmail' => '',
    'receivedPassword' => ''
);

$response['receivedEmail'] = $_POST['email'];
$response['receivedPassword'] = $_POST['password'];
?>
```
```js
    $(document).ready(function(){

        // 註冊事件
        $("#register-form").on('submit' ,function(e){
            e.preventDefault();

            $.ajax({
                type: "POST",
                url: "../../PHP/login-signup/register_process.php",
                data:new FormData($("#register-form")[0]),
                dataType: "json",
                contentType: false,
                cache:false,
                processData:false,
                error:function(){
                    alert("POST出錯");
                },
                success:function(response){
                    $(".form-message").css("display","block");
                    if(response.status == 1){
                        $("#main-signup").css("display","none");
                        $("#main-login").css("display","block");
                        $("#login-form")[0].reset();
                        $("#login-form .form-message").html('<p>' + response.message + '</p>');
                    }else{
                        $(".form-message").css("display","block");
                        $(".form-message").html('<p>' + response.message + '</p>');
                    }

                    setTimeout(function(){
                        $("#login-form .form-message").css("display","none");
                    }, 3000);
                }
            });
        });

        // 登入事件
        $("#login-form").on('submit', function(e){
            e.preventDefault();

            var data = {
                email: $("#login-user").val(),
                password: $("#login-password").val()
            };

            $.ajax({
                type: "POST",
                url: "../../PHP/login-signup/login_process.php",
                data: data,
                dataType: "json",
                cache:false,
                processData:false,
                error:function(jqXHR, textStatus, errorThrown){
                    console.log(jqXHR, textStatus, errorThrown);
                    alert("POST出錯");
                },
                success:function(response){
        
                    if(response.status == 1){
                        window.location.href = "../../PHP/Index/user_page.php";
                    }else{
                        console.log(data);
                        $(".form-message").css("display","block");
                        $(".form-message").html('<p>' + response.message + '</p>');
                    }

                    
                }
            });

        });
        
    });
```
<img src="https://github.com/THE-OCEAN0526/Studyed-Program-Language/assets/122972916/7f14d5f9-e6f0-40e2-a2fb-de7eefd348d7" width="500"><br>
URL用localhost試試，認PHP server沒問題
<img src="https://github.com/THE-OCEAN0526/Studyed-Program-Language/assets/122972916/e16e0c3f-44c4-490f-998b-7a0d8ddcc617" width="700"><br>
console出現PHP警告還有未是先確認email,password的存在
將PHP改這樣
```php
<?php
// header('Content-Type: text/html; charset=utf-8');
session_start();
require '../login-signup/config.php';

$response = array(
    'status' => 0,
    'message' => '沒收到',
    'receivedEmail' => isset($_POST['email']) ? $_POST['email'] : null,
    'receivedPassword' => isset($_POST['password']) ? $_POST['password'] : null
);

?>
```
然後就變這樣
<img src="https://github.com/THE-OCEAN0526/Studyed-Program-Language/assets/122972916/351de5db-6914-429e-adae-1ce9c844aa77" width="1000">

## 最終解答
ajax因為processData的問題，FormData不受 processData 的影響。
```js
 // 登入事件
        $("#login-form").on('submit', function(e){
            e.preventDefault();

            // var data = {
            //     email: $("#login-user").val(),
            //     password: $("#login-password").val()
            // };

            $.ajax({
                type: "POST",
                url: "../../PHP/login-signup/login_process.php",
                data: new FormData($("#login-form")[0]),
                dataType: "json",
                contentType: false,
                cache: false,
                processData: false,
                error:function(jqXHR, textStatus, errorThrown){
                    console.log(jqXHR, textStatus, errorThrown);
                    alert("POST出錯");
                },
                success:function(response){
        
                    if(response.status == 1){
                        $("#login-form")[0].reset();
                        window.location.href = "../../PHP/Index/user_page.php";
                    }else{
                        // console.log(response);
                        $(".form-message").css("display","block");
                        $(".form-message").html('<p>' + response.message + '</p>');
                    }

                    
                }
            });

        });
```
processData 是 jQuery Ajax 請求中的一個重要屬性，它控制著如何處理發送的數據。
默認情況下(false)，當你設置 data 屬性為一個對象時（比如 { key: value }），jQuery 不會將其轉換為查詢字符串格式。所以要改成true
然而，如果你發送的數據本身已經是預期的格式，比如 JSON 格式，你就需要將 processData 設置為 false，以避免 jQuery 對數據進行額外的處理。
