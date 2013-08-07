socket.on('chat', function(userid, username, _time, message){
    time = Date.parse(_time);
    $('#initial-message', $area).remove();
    if(username==="SERVER"){
      $area.append('<div class="message"><p><i>'+message+'</i></p></div>')
    }else{
      $area.append('<div class="message"><div class="avatar"><img src="/u/'+userid+'/image" /></div><div class="username">'+username+'</div><p>'+message+'</p><div class="time" data-time='+_time+'>'+time+'</div></div>')
    }
    // Scroll to show the next incoming message
    if (Date.now() - time <= 5000){
      $area.animate({scrollTop: $area[0].scrollHeight}, 250);
    }else{
      $area.scrollTop($area[0].scrollHeight);
    }
  })
 
 
  updateTimeStamps = function(){
    $('.message > .time').each(function(el){
      $el = $(el);
      time = $el.data('time')
      timeAgoString = getTimeAgo(time);
      $el.html(timeAgoString);
    })
  }
 
var getTimeAgo = function(originTime){
  var timeDifference = Date.now-originTime;
	if(timeDifference>60){
		if(timeDifference>3600){
			(return timeDifference/3600 % 3600).toFixed(0) + “hours”;
		}
		else{
			(return timeDifference/60 % 60).toFixed(0) + “minutes”;
		}
	}
	else{
		return timeDifference.toFixed(0)+"seconds";
	}
}
 
  setInterval(updateTimeStamps, 15000);
