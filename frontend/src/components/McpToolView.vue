<template>
  <div
    class="h-[36px] flex items-center px-3 w-full bg-[var(--background-gray-main)] border-b border-[var(--border-main)] rounded-t-[12px] shadow-[inset_0px_1px_0px_0px_#FFFFFF] dark:shadow-[inset_0px_1px_0px_0px_#FFFFFF30]">
    <div class="flex-1 flex items-center justify-center">
      <div class="max-w-[250px] truncate text-[var(--text-tertiary)] text-sm font-medium text-center">
        MCP Tool
      </div>
    </div>
  </div>
  <div class="flex-1 min-h-0 w-full overflow-y-auto">
    <div class="flex-1 min-h-0 max-w-[640px] mx-auto">
      <div class="flex flex-col overflow-auto h-full px-4 py-3">
        <div class="py-3 pt-0">
          <div class="text-[var(--text-primary)] text-sm font-medium mb-2">
            Tool: {{ toolContent.function }}
          </div>
          
          <!-- 显示参数 -->
          <div v-if="toolContent.args && Object.keys(toolContent.args).length > 0" class="mb-4">
            <div class="text-[var(--text-primary)] text-sm font-medium mb-2">Arguments:</div>
            <pre class="bg-[var(--fill-tsp-gray-main)] rounded-lg p-3 text-xs text-[var(--text-secondary)] overflow-x-auto"><code>{{ JSON.stringify(toolContent.args, null, 2) }}</code></pre>
          </div>
          
          <!-- 显示结果 -->
          <div v-if="toolContent.content?.result" class="mb-4">
            <div class="text-[var(--text-primary)] text-sm font-medium mb-2">Result:</div>
            <div class="bg-[var(--fill-tsp-gray-main)] rounded-lg p-3 text-sm text-[var(--text-secondary)] whitespace-pre-wrap">
              {{ toolContent.content.result }}
            </div>
          </div>
          
          <!-- 如果没有结果，显示状态 -->
          <div v-else class="text-[var(--text-tertiary)] text-sm">
            {{ toolContent.status === 'calling' ? 'Tool is executing...' : 'Waiting for result...' }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ToolContent } from '../types/message';

defineProps<{
  sessionId: string;
  toolContent: ToolContent;
  live: boolean;
}>();
</script> 