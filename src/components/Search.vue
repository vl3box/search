<template>
	<div class="m-search">
		<el-input :placeholder="$t('请输入内容')" v-model="q" class="input-with-select" @change="search" clearable>
			<el-select v-model="type" slot="prepend" :placeholder="$t('请选择')" class="m-search-type">
				<el-option :label="$t('全部')" value="all">{{ $t('全部') }}</el-option>
				<el-option :label="$t('作品')" value="post">{{ $t('作品') }}</el-option>
				<el-option :label="$t('百科')" value="wiki">{{ $t('百科') }}</el-option>
				<el-option :label="$t('用户')" value="author">{{ $t('用户') }}</el-option>
				<el-option :label="$t('谷歌')" value="google">Google</el-option>
			</el-select>
			<el-button slot="append" icon="el-icon-search"></el-button>
		</el-input>
	</div>
</template>

<script>
export default {
	name: "Search",
	props: [],
	data: function () {
		return {
			//搜索词
			q: "",
			//类型
			type: "",
		};
	},
	watch: {
		type: function () {
			this.$store.commit("changeType", this.type);
		},
	},
	methods: {
		search() {
			if (!this.q) return;
			this.$store.commit("changeQuery", this.q);
		},
		init() {
			let params = new URLSearchParams(location.search);
			this.q = params.get("q") || "";
			this.type = params.get("type") || "all";
			this.search();
		},
	},
	mounted: function () {
		this.init();
	},
};
</script>

<style lang="less">
//搜索框
.el-input-group__prepend .el-select {
	width: 80px;
}
.el-input-group__prepend .el-select:lang(vi) {
	width: 128px;
}
.el-select-dropdown__item img {
	width: @space;
	vertical-align: middle;
	position: relative;
	top: -2px;
	margin-right: 5px;
}
@media screen and (max-width: @ipad-y) {
	.m-search-type {
		display: none;
	}
}
</style>
