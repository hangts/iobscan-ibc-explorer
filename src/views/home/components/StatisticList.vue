<template>
    <div class="statistic_list">
        <!-- vertical -->
        <div v-if="type === 'vertical'" class="vertical_container">
            <div
                class="list_item ibc_selected_title"
                style="width: 100%"
                v-for="(item, name, index) of msg"
                :key="item.statistics_name"
                @click="clickListItem(item.statistics_name)"
            >
            <div class="list_item_info" :style="item.statistics_name === ibcStatisticsDenomsDefault['denom_all'].statistics_name ? 'cursor: text;' : ''">
                <span class="list_item_name"
                >{{
                        statisticsName[item.statistics_name]
                    }}<span v-if="item.statistics_name.indexOf('24') !== -1" class="list_item_tip"
                    >24hr</span
                    ></span
                >
                         <span class="list_item_value"  :style="item.statistics_name === ibcStatisticsDenomsDefault['denom_all'].statistics_name ? 'color: var(--bj-text-normal); cursor: text;' : ''">{{ `${formatBigNumber(item.count)}` }}</span>
            </div>
                <a-divider class="list_item_divider" v-show="index < Object.keys(msg).length - 1"/>
            </div>
        </div>

        <!-- horizontal -->
        <div v-if="type === 'horizontal'" class="horizontal_container">
            <div
                class="list_item_horizontal ibc_selected_title"
                v-for="(item, name, index) of msg"
                :key="item.statistics_name"
                @click="clickListItem(item.statistics_name)"
            >
                <div class="list_item">
                    <div class="list_item_info" :style="item.statistics_name === ibcStatisticsDenomsDefault['denom_all'].statistics_name ? 'cursor: text;' : ''">
                        <span class="list_item_name"
                        >{{
                                statisticsName[item.statistics_name]
                            }}<span v-if="item.statistics_name.indexOf('24') !== -1" class="list_item_tip"
                            >24hr</span
                            ></span
                        >
                                  <span class="list_item_value" :style="item.statistics_name === ibcStatisticsDenomsDefault['denom_all'].statistics_name ? 'color: var(--bj-text-normal);cursor: text;' : ''">{{ `${formatBigNumber(item.count)}` }}</span>
                    </div>
                </div>
                <a-divider
                    class="list_item_divider_vertical"
                    type="vertical"
                    v-show="index < Object.keys(msg).length - 1"
                />
            </div>
        </div>
    </div>
</template>

<script setup>
import {statisticsName, ibcStatisticsDenomsDefault} from '../../../constants/index';
import {formatBigNumber} from '../../../helper/parseString';
const props = defineProps({
    type: String,
    msg: Object
})
const emits = defineEmits(['clickItem'])
const clickListItem = (value) => {
    emits('clickItem', value);
};
</script>

<style lang="less" scoped>

.statistic_list {
    padding: 24px;
    width: 100%;
}

.vertical_container {
    .flex(column, nowrap, flex-start, flex-start);
}

.horizontal_container {
    .flex(row, nowrap, flex-start, flex-start);
}

.list_item {
    
    &_horizontal {
        width: 25%;
        .flex(row, nowrap, space-between, flex-start);
    }
    &_info {
        .flex(column, nowrap, flex-start, flex-start);
        
    }

    &_name {
        font-size: var(--bj-font-size-sub-title);
        font-family: Montserrat-Regular, Montserrat;
        color: var(--bj-font-color-65);
        line-height: var(--bj-font-size-sub-title);
        margin-bottom: 16px;
    }

    &_value {
        transition: color 0.3s;
        transition-timing-function: ease;
        font-size: var(--bj-font-size-home-number);
        font-family: Montserrat-Regular, Montserrat;
        color: var(--bj-text-normal);
        line-height: var(--bj-font-size-home-number);
    }

    &_tip {
        margin-left: 8px;
        padding: 0 4px;
        font-size: var(--bj-font-size-small);
        font-family: Montserrat-Regular, Montserrat;
        color: #3d50ff;
        line-height: var(--bj-font-size-small);
        background: rgba(61, 80, 255, 0.15);
        border-radius: 7px;
    }

    &_divider {
        width: 226px;
    }

    &_divider_vertical {
        height: 56px;
        margin-right: 24px;
    }
}
</style>
