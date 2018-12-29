<template>
  <div class="tagify-container">
		<transition-group tag="div" name="tagify-tag-animation" class="tagify">
			<span v-for="(tag, index) in tags" :key="tag" :class="{ active : selected === index }" class="tagify-tag">{{ tag }} <i @click="splice(index)" class="material-icons">close</i></span>
		</transition-group>
		<input type="text" @keyup.enter="push" @blur="push" v-model="tag" :placeholder="placeholder" class="tagify-input"/>
  </div>
</template>

<script>
	export default {
		name: 'Tagify',

		data: function() {
			return {
				tag: null
			}
		},

		props: {
			placeholder: {
				type: String,
				default: 'Type here...'
			},
			tags: {
				type: Array,
				default: []
			}
		},

		methods: {
			push: function() {
				if (this.tag && !this.tags.includes(this.tag)) {
					this.tags.push(this.tag);

					this.tag = null;
				}
			},
			splice: function(index) {
				this.tags.splice(index, 1);
			}
		}
	}
</script>

<style lang="scss">
    .tagify-container { cursor: text; padding: 0.25rem 0; background-color: #fff;
			.tagify { display:flex;
				&:after { content:''; clear:both; display:block; }
			}

			.tagify-tag, .tagify-input { font-size: 16px; }

			.tagify-tag { align-items:center; background-color: #fff; border:1px solid #d7dbe0; border-radius:16px; color:#444; display:flex; font-size:14px; height:32px; line-height:32px; margin:2px 4px 2px 0; padding:0 6px 0 12px; 
				&.active {
						color: #fff;
						background-color: #2196f3;
				}
				.material-icons { cursor: pointer; font-size: 20px; }
			}

			.tagify-tag-animation-enter-active { transition:all .2s; }
			.tagify-tag-animation-enter { opacity:0; transform:translateY(10px); }
			.tagify-tag-animation-enter-to { opacity:1; transform:translateY(-2px); }

			.tagify-input { border:none; height:32px; margin:2px 0; outline:none; padding:0; width:100%; }
    }
</style>
