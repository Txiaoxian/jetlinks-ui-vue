<!-- 操作记录 -->
<template>
    <page-container>
        <pro-search
            :columns="columns"
            target="record-search"
            @search="handleSearch"
        />
        <FullPage>
          <j-pro-table
              ref="RecordRef"
              :columns="columns"
              :request="queryList"
              :defaultParams="{
                      pageSize: 10,
                      sorts: [{ name: 'time', order: 'desc' }],
                  }"
              :pagination="{
                      showSizeChanger: true,
                      pageSizeOptions: ['10', '20', '50', '100'],
                  }"
              :params="params"
              :model="'TABLE'"
          >
              <template #time="slotProps">
                  {{
                      slotProps.time
                          ? moment(slotProps.time).format('YYYY-MM-DD HH:mm:ss')
                          : ''
                  }}
              </template>
          </j-pro-table>
        </FullPage>
    </page-container>
</template>

<script setup lang="ts">
import { queryList } from '@/api/iot-card/record';
import moment from 'moment';

const params = ref<Record<string, any>>({});

const columns = [
    {
        title: '卡号',
        dataIndex: 'cardId',
        key: 'cardId',
        ellipsis: true,
        search: {
            type: 'string',
        },
    },
    {
        title: '操作类型',
        dataIndex: 'type',
        key: 'type',
        search: {
            type: 'string',
        },
    },
    {
        title: '操作时间',
        dataIndex: 'time',
        key: 'time',
        scopedSlots: true,
        search: {
            type: 'date',
        },
    },
    {
        title: '操作人',
        dataIndex: 'operator',
        key: 'operator',
        ellipsis: true,
        search: {
            type: 'string',
        },
    },
];

const handleSearch = (e: any) => {
    params.value = e;
};
</script>

<style scoped lang="less"></style>
