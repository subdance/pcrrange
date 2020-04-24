<template>
	<div class="main-container">
		<div class="character-holder">
			<div 
				class="single-character"
				v-for="(item, index) in info" 
				:key="index"
				@click="push(item)"
				>
				<div class="avatar">
					<img :src="item.avatar" alt="">
				</div>
				<div class="name">
					{{item.name}}
				</div>
				<div class="range">
					{{item.range}}
				</div>
			</div>
		</div>
		<div class="range-indicator">
			<div 
				class="range-diff"
				v-for="(item, index) in rangeDiff" 
				:key="index"
				:v-if="index != 0"
				>
				{{item}}
			</div>
		</div>
		<div class="result-holder">
			<div 
				class="single-result"
				v-for="(item, index) in queue" 
				:key="index"
				@click="remove(index)"
				>
				<img :src="item.avatar" alt="">
				<div class="name-holder">
					{{item.name}}
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			counter: 0,
			queue: [],
			rangeValue: [],
			rangeDiff: [],
			info:[{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_105231.png","name":"莉瑪","range":"105"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_100731.png","name":"宮子","range":"125"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_104531.png","name":"空花","range":"130"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_104731.png","name":"純","range":"135"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_109531.png","name":"空花（大江戶）","range":"140"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_101731.png","name":"香織","range":"145"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_108931.png","name":"怜（新年）","range":"153"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_112531.png","name":"リン（デレマス）","range":"153"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_105831.png","name":"貪吃佩可","range":"155"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_180431.png","name":"ペコリーヌ（プリンセス）","range":"155"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_105631.png","name":"流夏","range":"158"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_111931.png","name":"コッコロ（ニューイヤー）","range":"159"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_102931.png","name":"望","range":"160"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_106131.png","name":"矛依未","range":"162"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_104331.png","name":"真琴","range":"165"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_106531.png","name":"嘉夜","range":"168"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_108731.png","name":"日和（新年）","range":"170"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_109631.png","name":"妮諾（大江戶）","range":"175"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_103231.png","name":"秋乃","range":"180"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_110431.png","name":"真琴（夏日）","range":"180"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_100531.png","name":"茉莉","range":"185"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_110831.png","name":"克蘿依","range":"185"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_109031.png","name":"惠理子（情人節）","range":"187"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_108631.png","name":"綾音（聖誕節）","range":"190"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_105431.png","name":"紡希","range":"195"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_100131.png","name":"日和","range":"200"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_100431.png","name":"禊","range":"205"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_102331.png","name":"綾音","range":"210"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_111231.png","name":"禊（萬聖節）","range":"212"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_104631.png","name":"珠希","range":"215"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_103731.png","name":"智","range":"220"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_110931.png","name":"琪愛兒","range":"222"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_107931.png","name":"珠希（夏日）","range":"225"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_102731.png","name":"惠理子","range":"230"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_107531.png","name":"貪吃佩可（夏日）","range":"235"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_102131.png","name":"胡桃","range":"240"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_105731.png","name":"吉塔","range":"245"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_100331.png","name":"怜","range":"250"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_111731.png","name":"伊莉亞（聖誕節）","range":"255"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_111531.png","name":"克莉絲提娜（聖誕節）","range":"265"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_104931.png","name":"靜流","range":"285"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_107131.png","name":"克莉絲提娜","range":"290"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_108531.png","name":"胡桃（聖誕節）","range":"295"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_102031.png","name":"美美","range":"360"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_103131.png","name":"忍","range":"365"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_111331.png","name":"美美（萬聖節）","range":"365"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_112431.png","name":"ウヅキ（デレマス）","range":"370"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_109131.png","name":"靜流（情人節）","range":"385"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_103331.png","name":"真陽","range":"395"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_103431.png","name":"優花梨","range":"405"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_105331.png","name":"莫妮卡","range":"410"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_103031.png","name":"妮諾","range":"415"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_111631.png","name":"望（聖誕節）","range":"418"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_104831.png","name":"美冬","range":"420"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_104431.png","name":"伊莉亞","range":"425"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_110531.png","name":"香織（夏日）","range":"425"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_102831.png","name":"咲戀","range":"430"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_100931.png","name":"杏奈","range":"440"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_108131.png","name":"忍（萬聖節）","range":"440"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_108031.png","name":"美冬（夏日）","range":"495"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_105931.png","name":"可可蘿","range":"500"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_105531.png","name":"步未","range":"510"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_109431.png","name":"古蕾婭","range":"525"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_107631.png","name":"可可蘿（夏日）","range":"535"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_109731.png","name":"雷姆","range":"540"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_109831.png","name":"拉姆","range":"545"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_102631.png","name":"鈴","range":"550"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_105131.png","name":"深月","range":"565"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_100631.png","name":"茜里","range":"570"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_102231.png","name":"依里","range":"575"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_110331.png","name":"咲戀（夏日）","range":"585"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_108231.png","name":"宮子（萬聖節）","range":"590"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_106331.png","name":"亞里莎","range":"625"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_109231.png","name":"安","range":"630"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_109331.png","name":"露","range":"640"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_107031.png","name":"似似花","range":"660"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_110731.png","name":"碧（插班生）","range":"680"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_112031.png","name":"キャル（ニューイヤー）","range":"690"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_112631.png","name":"ミオ（デレマス）","range":"695"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_101131.png","name":"璃乃","range":"700"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_101631.png","name":"鈴奈","range":"705"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_110031.png","name":"鈴奈（夏日）","range":"705"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_103831.png","name":"栞","range":"710"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_112331.png","name":"シオリ（マジカル）","range":"712"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_101831.png","name":"伊緒","range":"715"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_110131.png","name":"伊緒（夏日）","range":"715"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_102531.png","name":"鈴莓","range":"720"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_112131.png","name":"スズメ（ニューイヤー）","range":"722"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_109931.png","name":"愛蜜莉雅","range":"725"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_101431.png","name":"霞","range":"730"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_112231.png","name":"カスミ（マジカル）","range":"730"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_101531.png","name":"美里","range":"735"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_101331.png","name":"七七香","range":"740"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_108831.png","name":"優衣（新年）","range":"745"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_106031.png","name":"凱留","range":"750"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_101231.png","name":"初音","range":"755"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_105031.png","name":"美咲","range":"760"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_111431.png","name":"露娜","range":"765"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_108431.png","name":"千歌（聖誕節）","range":"770"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_107731.png","name":"鈴莓（夏日）","range":"775"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_107831.png","name":"凱留（夏日）","range":"780"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_104031.png","name":"碧","range":"785"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_104231.png","name":"千歌","range":"790"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_110631.png","name":"真步（夏日）","range":"792"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_101031.png","name":"真步","range":"795"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_100231.png","name":"優衣","range":"800"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_100831.png","name":"雪","range":"805"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_111031.png","name":"優妮","range":"807"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_103631.png","name":"鏡華","range":"810"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_108331.png","name":"美咲（萬聖節）","range":"815"},{"avatar":"https://pcredivewiki.tw/static/images/unit/icon_unit_111131.png","name":"鏡華（萬聖節）","range":"820"}]
		}
	},
	methods: {
		push(item) {
			if (this.counter === 5) return;
			const index = this.queue.map(innerItem => innerItem.name).indexOf(item.name);
			if (index != -1) {
				this.remove(index);
			}
			else {
				this.queue.push(item);
				this.queue.sort((pre, next) => Number(pre.range)-Number(next.range));
				this.measureRange();
				this.counter ++;
			}
		},
		remove(index) {
			this.rangeValue.splice(index, 1);
			this.queue.splice(index, 1);
			this.measureRange();
			this.counter --;
		},
		measureRange() {
			let temp = this.queue.map((item, index) => {
				if (index == 0) {
					return 0
				}
				else {
					return Number(this.queue[index].range) - Number(this.queue[index - 1].range);
				}
			})
			temp.shift();
			this.rangeDiff = temp;
		}
	}
}
</script>

<style lang="scss" scoped>
	.main-container {
		padding-top: 20px;
		text-align: center;
		width: 100%;
		max-width: 1000px;
		margin: auto;
		overflow: hidden;

		.character-holder {
			display: flex;
			flex-flow: row wrap;
			margin-bottom: 180px;
			width: 100%;
			justify-content: center;

			.single-character {
				margin-left: 10px;
				margin-top: 10px;
				width: 90px;
				display: flex;
				flex-flow: column nowrap;
				padding-top: 2px;
				cursor: pointer;
				transition: 0.2s all;
				color: #f25d8e;
				background-color: white;
				padding: 4px 2px;
				box-shadow: 2px 2px 2px grey;
				
				&:hover {
				box-shadow:
					0 2.8px 2.2px rgba(0, 0, 0, 0.02),
					0 6.7px 5.3px rgba(0, 0, 0, 0.028),
					0 12.5px 10px rgba(0, 0, 0, 0.035),
					0 22.3px 17.9px rgba(0, 0, 0, 0.042),
					0 41.8px 33.4px rgba(0, 0, 0, 0.05),
					0 100px 80px rgba(0, 0, 0, 0.07);
					transition: 0.2s all;
					transform: scale(1.1);
				}

				.name {
					text-overflow: ellipsis;
					overflow: hidden;
					white-space: nowrap;
					font-size: 16px;
					line-height: 16px;
					padding: 2px 0px;
				}
				.range {
					padding: 2px 0px;
					line-height: 16px;
				}
				.avatar {

					img {
						width: 80px;
						display: block;
						margin: auto;
					}
				}
			}
		}

		.range-indicator {
			width: 80%;
			max-width: 500px;
			height: 20px;
			line-height: 20px;
			position: fixed;
			bottom: 135px;
			left: 50%;
			transform: translate(-50%, 0);
			display: flex;
			flex-flow: row-reverse nowrap;
			background-color: rgba($color: #000000, $alpha: 0.5);
			justify-content: space-evenly;
			&::after {
				content: "相邻角色距离差:";
				position: absolute;
				left: -120px;
				color: #00b6ff;
				font-weight: bold;
			}

			.range-diff {
				color: white;
				flex: 0 0 30px
			}
		}

		.result-holder {
			border-radius: 5px;
			position: fixed;
			bottom: 5px;
			width: 95%;
			max-width: 540px;
			height: 110px;
			left: 50%;
			transform: translate(-50%, 0);
			backdrop-filter: blur(4px);
			display: flex;
			flex-flow: row-reverse nowrap;
			align-items: center;
			box-shadow: 0px 0px 2px black;
			padding: 3px;
			justify-content: space-evenly;

			.single-result {
				position: relative;
				width: 20%;
				max-width: 100px;
				max-height: 100px;
				box-sizing: border-box;
				cursor: pointer;
				transition: 0.2s all;
				filter: drop-shadow(0 0 4px #00b6ff);
				border-radius: 0 0 5px 5px;
				// overflow: hidden;
				&:not(:first-of-type) {
					margin-right: 10px;
				}
				&:hover {
					// filter: drop-shadow(0 0 6px crimson);
					transition: 0.2s all;
				}

				img {
					width: 100%;
					display: block;
				}
				.name-holder {
					position: absolute;
					bottom: 0px;
					left: 0px;
					width: 100%;
					height: 18px;
					color: white;
					font-size: 13px;
					line-height: 18px;;
					background-color: rgba($color: #000000, $alpha: 0.5);
					overflow: hidden;
				}
			}

		}
	}
	@media screen and (max-width: 590px) {
		.range-indicator::after {
			content: ""!important;
		}
		.result-holder {
			max-height: 80px!important;
			backdrop-filter: blur(0px)!important;
			background-color: rgba($color: #000000, $alpha: 0.5)
		}
		.range-indicator {
			bottom: 100px!important;
		}
		.single-result {
			border: 1px solid #f25d8e;
			filter: none!important;
		}
		.single-result:hover {
			filter: none!important;
		}
	}
</style>