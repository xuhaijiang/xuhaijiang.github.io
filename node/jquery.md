##### 判断是否隐藏
    $("#otherInfo").is(":hidden")
     
    $("#otherInfo").show();
     
    $("#otherInfo").hide();

##### 单选
    var consSex = $('input:radio[name="consSex"]:checked').val();
    
    <div class="box">客户性别：
     <input type="radio" name="consSex" value="男" />男
     <input type="radio" name="consSex" value="女" />女
    </div>