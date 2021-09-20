<html lang="en">
<head>
<title>Trends</title>
</head>
	<style>
a:link {
  color: brown;
}
	</style>
<body>
<div id="catagoryname">
	<h1>India - Trending Music Videos</h1>
</div>
<div id="trending"></div>
<script  type='text/javascript' src='https://code.jquery.com/jquery-3.6.0.js'></script>
<script  type='text/javascript' src='dateformat.min.js'></script>
	
<script>
var maxVideos = 30;
$(document).ready(function() {
	$.get(
		"https://www.googleapis.com/youtube/v3/videos", {
			part: 'snippet,statistics',
			chart: 'mostPopular',
			kind: 'youtube#videoListResponse',
			maxResults: maxVideos,
			regionCode: 'IN',
			videoCategoryId: 10,
			hl: "kn-IN",
			key: 'AIzaSyDOYHC18HA_vSAcs8a7yrxKiwBw1wLfAvk'
		},
		function(data) {
			var output = '<table border=1><thead><tr><th>#</th><th>Thumb</th><th>Title</th><th>Views</th><th>Likes</th><th>Dislikes</th><th>Comments</th><th>Published On</th></tr></thead><tbody>';
			$.each(data.items, function(i, item) {
				vidId = item.id;
				videTitle = item.snippet.title;
				description = item.snippet.description;
				thumb = item.snippet.thumbnails.high.url;
				channelTitle = item.snippet.channelTitle;
				videoDate = item.snippet.publishedAt;
				Catagoryid = item.snippet.categoryId;
				channelId = item.snippet.channelId;
				cID = item.snippet.channelId;
				views = numberWithCommas(item.statistics.viewCount);
				likes = numberWithCommas(item.statistics.likeCount);
				dislikes = numberWithCommas(item.statistics.dislikeCount);
				comment = numberWithCommas(item.statistics.commentCount);
				publishedAt = item.snippet.publishedAt + "+05:30";
				publishedAt = $.format.date(publishedAt, "dd/MM/yyyy hh:mm:ss a");
				var style = "";
				if (videTitle.toLowerCase().includes("himesh")) {
					style = "style='background: #d4ffdf;' ";
				}
				videTitle = "<a target='_blank' href='https://www.youtube.com/watch?v=" + vidId + "'>" + videTitle + "</a>";
				thumb = "<img style='padding:2px;' src='" + item.snippet.thumbnails.default.url + "' width='120' height='90'/>";
				output += '<tr ' + style + '><td>' + ++i + '</td><td>' + thumb + '</td><td>' + videTitle + '</td><td>' + views + '</td><td>' + likes + '</td><td>' + dislikes + '</td><td>' + comment + '</td><td>' + publishedAt + '</td></tr>';
			
				/*$.get("https://www.googleapis.com/youtube/v3/channels", {
					part: 'snippet,statistics',
					id: channelId,
					key: 'AIzaSyDOYHC18HA_vSAcs8a7yrxKiwBw1wLfAvk'
				},
				function(data) {
					output += '<td>' + data.items[0].statistics.subscriberCount + '</td>';
				});*/
			})

			
			output += '</tbody></table>';
			$('#trending').append(output);
		}
	);
});

function numberWithCommas(x) {
	if(x != null)
	{
    return x.toString().split('.')[0].length > 3 ? x.toString().substring(0,x.toString().split('.')[0].length-3).replace(/\B(?=(\d{2})+(?!\d))/g, ",") + "," + x.toString().substring(x.toString().split('.')[0].length-3): x.toString();
	}
} 
</script>
</body>
</html>
