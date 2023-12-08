# GET

1. 详情页面 /api/v1/activity/<int:id>

   ```json
   {
       id: 活动的ID，跟在路径后面
   }
   ```

   

2. 获取页面列表 /api/v1/activity

   ```json
   {
       user_id: 活动发起人的ID， 可选
       keyword: 关键词（后端会对活动所有文本进行模糊搜索），可选
       label: 标签（后端会对活动的主题分类进行模糊搜索），可选
       status: 卡片的状态（三种）可选
       page_on: 页码，必选
       page_size: 页面大小，默认为20，可选
   }
   说明：如果只有page_on和page_size参数，后端将返回所有的活动。
   ```

   

3. 详情页面（组队）/api/v1/team/<int:id>

   ```json
   {
       id: 活动的ID，跟路径后面
   }
   ```

   

4. 获取页面列表（组队）/api/v1/team

   ```json
   {
       user_id: 活动发起人的ID， 可选
       keyword: 关键词（后端会对活动所有文本进行模糊搜索），可选
       label: 标签（后端会对活动的主题分类进行模糊搜索），可选
       status: 卡片的状态（三种）可选
       page_on: 页码，必选
       page_size: 页面大小，默认为20，可选
   }
   说明：如果只有page_on和page_size参数，后端将返回所有的活动。
   ```

   

---

# POST

1. 添加活动卡片 /api/v1/activity/release

   ```json
   {
       title: 标题，必选
       label: 主题分类，必选
       content: 活动介绍，必选
       address: 活动地址，可选
       activity_time: 活动时间，必选
       deadline: 截止时间，必选
       card_status: 活动卡片的状态（三种），必选
   }
   ```

   

2. 添加组队卡片 /api/v1/team/release

   ```json
   {
       title: 标题，必选
       label: 主题分类，必选
       team_name: 队伍名字，必选
       content: 活动介绍，必选
       address: 活动地址，可选
       activity_time: 活动时间，必选
       deadline: 截止时间，必选
       card_status: 活动卡片的状态（三种），必选
   }
   ```

---

# PUT

1. 修改草稿状态的活动卡片 /api/v1/activity

   ```json
   {
       card_id: 活动ID，必选
       card_status: 活动状态（三种），必选
       label: 主题分类，可选
       title: 标题，可选
       content: 内容简介，可选
       address: 活动地址，可选
       activity_time: 活动时间，必选
       deadline: 截止时间，必选
   }
   ```

   

2. 修改草稿状态的组队卡片 /api/v1/team

   ```json
   {
       card_id: 活动ID，必选
       card_status: 活动状态（三种），必选
       label: 主题分类，可选
       title: 标题，可选
       team_name: 队伍名字，可选
       content: 内容简介，可选
       address: 活动地址，可选
       activity_time: 活动时间，必选
       deadline: 截止时间，必选
   }
   ```

   

---

# DELETE

1. 删除活动卡片 /api/v1/activity

   ```json
   {
       card_id: 活动ID， 必选
   }
   ```

   

2. 删除组队卡片 /api/v1/team

   ```json
   {
       card_id: 活动ID， 必选
   }
   ```

   