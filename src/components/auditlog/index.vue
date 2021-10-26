<template>
    <el-container>
        <el-main>
            <Split :gutterSize="5">
                <SplitArea :size="sizes[0]" :minSize="0" style="overflow:hidden;background:#f2f2f2;">
                    <TagTreeView :model="{domain:'auditlog'}" :fun="onRefreshByTag" ref="auditlogTagTree"></TagTreeView>
                </SplitArea>
                <SplitArea :size="sizes[1]" :minSize="0" style="overflow:hidden;">
                    <LogView ref="logView"></LogView>
                </SplitArea>
            </Split>
        </el-main>
    </el-container>
</template>

<script>

    import TagTreeView from '../tags/TagTreeView.vue';
    import LogView from './log.vue';
    export default {
        components:{
            TagTreeView,
            LogView
        },
        data(){
            return {
                sizes: [20,80]
            }
        },
        methods:{
            onRefreshByTag(tag){
                if(!tag){
                    this.$refs.logView.onSearch();
                } else {
                    this.$refs.logView.search.term = `tags=${tag}`;
                    this.$refs.logView.onSearch();
                }
            }
        }
    }
</script>

<style scoped>
    .el-main{
        padding:0px;
    }
</style>