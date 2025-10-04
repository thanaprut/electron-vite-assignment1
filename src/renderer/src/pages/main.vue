<template>
    <main>
        <div class="p-4 mx-auto max-w-(--breakpoint-2xl) md:p-6">
            <div
                class="overflow-hidden rounded-2xl border border-gray-200 bg-white p-5 dark:border-gray-800 dark:bg-white/[0.03] lg:p-6">
                <div class="flex flex-col gap-2 mb-4 sm:flex-row sm:items-center sm:justify-between">
                    <div>
                        <h3 class="font-outfit text-lg font-semibold text-gray-800 dark:text-white/90">
                            Process Input
                        </h3>
                    </div>
                    <div class="flex items-center gap-3">
                        <button @click="onClickAdd()" id="button"   type="button"
                            class="inline-flex items-center gap-2 px-4 py-3 text-sm font-medium text-white text-theme-sm font-medium text-gray-700 transition rounded-lg bg-brand-500 shadow-theme-xs hover:bg-brand-600">
                            Add
                        </button>
                
                        <label class="inline-flex items-center gap-2 rounded-lg border border-gray-300 bg-white px-4 py-2.5 text-theme-sm font-medium text-gray-700 shadow-theme-xs hover:bg-gray-50 hover:text-gray-800 dark:border-gray-700 dark:bg-gray-800 dark:text-gray-400 dark:hover:bg-white/[0.03] dark:hover:text-gray-200 cursor-pointer">
                            <input 
                                type="file" 
                                accept=".csv" 
                                class="hidden"
                                @change="handleFileUpload"
                            />
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                            stroke="currentColor" class="stroke-current fill-white dark:fill-gray-800 size-4">
                                <path stroke-linecap="round" stroke-linejoin="round"
                                    d="M16.023 9.348h4.992v-.001M2.985 19.644v-4.992m0 0h4.992m-4.993 0 3.181 3.183a8.25 8.25 0 0 0 13.803-3.7M4.031 9.865a8.25 8.25 0 0 1 13.803-3.7l3.181 3.182m0-4.991v4.99" />
                            </svg>
                            Upload File
                        </label>
                        
                        <button
                            @click="this.$emit('reset');"
                            class="inline-flex items-center gap-2 rounded-lg border border-gray-300 bg-white px-4 py-2.5 text-theme-sm font-medium text-gray-700 shadow-theme-xs hover:bg-gray-50 hover:text-gray-800 dark:border-gray-700 dark:bg-gray-800 dark:text-gray-400 dark:hover:bg-white/[0.03] dark:hover:text-gray-200">
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                                stroke="currentColor" class="stroke-current fill-white dark:fill-gray-800 size-4">
                                <path stroke-linecap="round" stroke-linejoin="round"
                                    d="M16.023 9.348h4.992v-.001M2.985 19.644v-4.992m0 0h4.992m-4.993 0 3.181 3.183a8.25 8.25 0 0 0 13.803-3.7M4.031 9.865a8.25 8.25 0 0 1 13.803-3.7l3.181 3.182m0-4.991v4.99" />
                            </svg>
                            Reset
                        </button>
                    </div>
                </div>
                <div class="rounded-2xl h-120 scroll-small bg-gray-100 border-gray-200 border dark:border-gray-800">
                    <div class="w-full rounded-2xl h-100 bg-white px-5 pt-2 pb-2">
                        <div class="overflow-y-auto overflow-x-hidden scroll-small w-full h-full pr-5 pb-5 rounded-2xl">
                            <div class="grid  grid-cols-1 gap-4">
                                <slot/>
                            </div>
                        </div>
                    </div>
                    <div class="w-full rounded-2xl h-20">
                        <div class="w-full h-full flex items-center justify-center">
                            <button type="button"
                                @click="onCalculate"
                                class="inline-flex items-center gap-2 rounded-lg border border-gray-300 bg-white px-4 py-2.5 text-theme-sm font-medium text-gray-700 shadow-theme-xs hover:bg-gray-50 hover:text-gray-800 dark:border-gray-700 dark:bg-gray-800 dark:text-gray-400 dark:hover:bg-white/[0.03] dark:hover:text-gray-200">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
                                    stroke-width="1.5" stroke="currentColor"
                                    class="stroke-current fill-white dark:fill-gray-800 size-4">
                                    <path stroke-linecap="round" stroke-linejoin="round"
                                        d="M8.25 3v1.5M4.5 8.25H3m18 0h-1.5M4.5 12H3m18 0h-1.5m-15 3.75H3m18 0h-1.5M8.25 19.5V21M12 3v1.5m0 15V21m3.75-18v1.5m0 15V21m-9-1.5h10.5a2.25 2.25 0 0 0 2.25-2.25V6.75a2.25 2.25 0 0 0-2.25-2.25H6.75A2.25 2.25 0 0 0 4.5 6.75v10.5a2.25 2.25 0 0 0 2.25 2.25Zm.75-12h9v9h-9v-9Z" />
                                </svg>

                                Run Scheduler
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </main>
</template>
<script>
export default {
    props: ['onClickAdd', 'processList', 'onCalculate'],
    emits: ['file-uploaded', 'reset', 'deleteProcess'], 
    methods: {
        handleFileUpload(event) {
            const file = event.target.files[0];
            if (!file) return;
            
            const reader = new FileReader();
            
            reader.onload = (e) => {
                const text = e.target.result;
                const data = this.parseCSV(text);
                this.$emit('file-uploaded', data);
            };
            
            reader.readAsText(file);
        },
        parseCSV(text) {
            const lines = text.split('\n').filter(line => line.trim() !== '');
            const headers = lines[0].split(',').map(h => h.trim());
            
            const result = [];
            
            for (let i = 1; i < lines.length; i++) {
                const values = lines[i].split(',').map(v => v.trim());
                
                const obj = {
                    pid: values[0],                
                    arrival: Number(values[2]),      
                    burst: Number(values[1]),        
                    priority: Number(values[3])      
                };
                
                result.push(obj);
            }
            
            return result;
        }
    },
}
</script>