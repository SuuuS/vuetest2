<template>
	<div id="secondComponent">
		<h1>我是另一个页面</h1>
		<a>作者 {{author}}</a>
		<p>这些页面都是根据<a href="http://www.jianshu.com/p/5ba253651c3b">JinkeyBlog</a>大神的文章学习来的。</p>
		<p>↓ 来给articles:[]整点动态的数据</p>
		<ul>
			<li v-for="article in articles">
				{{article.title}}
			</li>
		</ul>
		<el-card class="box-card">
			<div slot="header" class="clearfix">
				<h2 style="line-height:36px;color:#20a0ff">豆瓣电影排行榜</h2>
			</div>
			<div v-for="article in articles" class="text item">
				{{article.title}}
			</div>
		</el-card>
	</div>
</template>

<script type="text/javascript">
	export default {
		data(){
			return {
				author : "微信公众号：XXX",
				articles:[]
			}
		},
		mounted:function(){
			this.$http.jsonp('https://api.douban.com/v2/movie/top250?count=10',{},{
				headers:{

				},
				emulateJSON:true
			}).then(function(response){
				//这里处理正确的回调
				this.articles = response.data.subjects;
				//this.articles = response.data["subjects"]也可以
				
			},function(response){
				//处理错误的回调
				console.log(response);
			});
		}
	}
</script>

<style type="text/css">
</style>