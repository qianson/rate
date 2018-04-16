<template>
  <div id="evaluate">
    <i class="iconfont icon-xingji solid" v-for="(star,index) in solidArr" :key="star.id" @click.stop.self='solid(index)'></i><i @click.stop.self="hollow(index)" class="iconfont icon-favorite hollow" v-for="(star,index) in hollowArr" :key="star.id"></i><span v-if="descShow">{{getStarDesc}}</span>
  </div>
</template>
<script>
export default {
    name: 'evaluate',
    props: {
        descShow: {
            type: Boolean,
            default: false
        }
    },
    data () {
        return {
            solidArr: [],
            hollowArr: [],
            solidNum: 0,
            hollowNum: 5,
            starDesc: ''
        };
    },
    created () {
        this.getHollowArr(5);
    },
    methods: {
        getSolidArr () {
            this.solidArr = [];
            for (let i = 1;i <= this.solidNum;i++) {
                let obj = {};
                obj.num = i;
                obj.id = 'solid' + i;
                this.solidArr.push(obj);
            }
        },
        getHollowArr () {
            this.hollowArr = [];
            this.solidArr = [];
            for (let i = 1;i <= this.hollowNum;i++) {
                let obj = {};
                obj.num = i;
                obj.id = 'hollow' + i;
                this.hollowArr.push(obj);
            }
        },
        solid (index) { // 点击实五角
            this.hollowNum = 4 - index;
            this.solidNum = index + 1;
            this.getHollowArr(this.hollowNum);
            this.getSolidArr();
            this.$emit('starOut', this.solidNum);
        },
        hollow (index) { // 点击空五角
            this.solidNum = this.solidNum + index + 1;
            this.hollowNum = 5 - this.solidNum;
            this.getHollowArr();
            this.getSolidArr();
            this.$emit('starOut', this.solidNum);
        }
    },
    computed: {
        getStarDesc () {
            switch (this.solidNum) {
            case 1:
                return '极差';
            case 2:
                return '失望';
            case 3:
                return '一般';
            case 4:
                return '满意';
            case 5:
                return '很好';
            }
        }
    }
};
</script>
<style lang='less'>
#evaluate{
  display: inline-block;
}
.solid,.hollow{
  margin-right:12px;
  color:#ED5566;
}
</style>
