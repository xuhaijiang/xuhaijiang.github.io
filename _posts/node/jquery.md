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

##### 下拉框
    $("#driverFlag").change(function(){
     var flagValue =   $("#driverFlag").find("option:selected").val();
    });

##### 时间
    function CurentTime()
    {
    var now = new Date();
    var year = now.getFullYear(); //年
    var month = now.getMonth() + 1; //月
    var day = now.getDate(); //日
    
    var hh = now.getHours(); //时
    var mm = now.getMinutes(); //分
    var ss = now.getSeconds(); //秒
    
    var clock = year + "-";
      
    if(month < 10)
     clock += "0";
      
    clock += month + "-";
      
    if(day < 10)
     clock += "0";
      
    clock += day + " ";
      
    if(hh < 10)
     clock += "0";
      
    clock += hh + ":";
    if (mm < 10) clock += '0';
    clock += mm;
    
    clock += ":";
    if (ss < 10) clock += '0';
    clock += ss;
    
    
    $("#startTime").val(clock);
    return(clock);
    }

####