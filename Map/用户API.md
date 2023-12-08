# 用户的api



## post

1. 注册  /api/v1/user/register

   1. post 参数模板

      ```json
      {
          username: 用户名，必选 
          gender: 性别， 必选（常量值里面的三个选项，男（1），女（2），不明（0））
          college: 学院，必选
          resident_campus: 校区，必选
          contact: 电话号码，必选
          password: 密码， 必选
          resume: 简历，可选
      }
      ```

2.  登录  /api/v1/user/login

   1.  post 参数模板

      ```json
      {
          contact/student_id: 电话号码和学号选一个
          password: 密码，必选
      }
      ```

      

3.  认证 /api/v1/user/verified

   1. post 参数模板

      ```
      {
          real_name: 真实姓名，必选
          student_id: 学生ID号，必选
          email: 邮箱，必选
          auth_code: 验证码，必选
      }
      ```

4. 验证码 /api/v1/user/auth

   1. post请求参数模板

      ```json
      {
          email: 邮箱，必选
      }
      ```

      

5. 重置密码 /api/v1/user/reset

   1. post请求参数模板

      ```json
      {
          pre_password: 之前的密码，必选
          new_password: 新的密码，必选
      }
      ```

   

   ---

   ## GET

   1. 获取用户资料 /api/v1/user

      1. get 请求参数模板

         ```json
         {
             user_id: 用户ID，可选
             contact: 联系方式，可选
             page_on: 页码，可选
             page_size: 页的大小，可选（page_on 和page_size应该同时传进来）
         }
         ```

   2. 注销 /api/v1/user/logout

   3. 获取指定用户的全部参与活动 /api/v1/user/activity

   4. 获取指定用户的全部参与组队 /api/v1/user/team

   ---

   ## PUT

1. 更新用户的资料 /api/v1/user

   1. put 请求参数模板

      ```json
      {
          username: 用户名，可选
          gender: 性别，可选
          college: 院校，可选
          resident_campus: 校区，可选
          contact: 电话号码，可选
          resume: 简历，可选
          real_name: 真实姓名， 可选
          email： 邮箱，可选
          student_id：学生ID，可选
      }
      ```

      

2. 报名活动 /api/v1/user/activity

   1. put 请求参数模板

      ```json
      {
          card_id: 活动ID，必选
      }
      ```

      

3. 报名组队 /api/v1/user/team

   1. put请求参数模板

      ```json
      {
          card_id: 活动ID，必选
      }
      ```

      

---

## DELETE

1. 退出活动 /api/v1/user/activity

   1. delete请求参数

      ```json
      {
          card_id: 活动ID，必选
      }
      ```

      

2. 退出组队 /api/v1/user/team

   1. delete请求参数模板

      ```json
      {
          card_id: 活动ID，必选
      }
      ```

      