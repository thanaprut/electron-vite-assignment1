<template>
    <main v-if="result && result?.processes">
        <div class="p-4 mx-auto max-w-(--breakpoint-2xl) md:p-6">
            <div class="overflow-hidden rounded-2xl border border-gray-200 bg-white p-5 dark:border-gray-800 dark:bg-white/[0.03] lg:p-6">
                <div class="flex flex-col gap-2 mb-4 sm:flex-row sm:items-center sm:justify-between">
                    <div>
                        <h3 class="font-outfit text-lg font-semibold text-gray-800 dark:text-white/90">
                            Performance Metrics
                        </h3>
                    </div>
                    <div class="flex items-center gap-3">
                        <button
                            @click="downloadCSV(result?.processes)"
                            class="inline-flex items-center gap-2 rounded-lg border border-gray-300 bg-white px-4 py-2.5 text-theme-sm font-medium text-gray-700 shadow-theme-xs hover:bg-gray-50 hover:text-gray-800 dark:border-gray-700 dark:bg-gray-800 dark:text-gray-400 dark:hover:bg-white/[0.03] dark:hover:text-gray-200">
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="stroke-current fill-white dark:fill-gray-800 size-4">
                                <path stroke-linecap="round" stroke-linejoin="round" d="m9 12.75 3 3m0 0 3-3m-3 3v-7.5M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
                            </svg>
                            Download
                        </button>
                        <button
                            @click="this.$emit('goToPage', 'main');"
                            class="inline-flex items-center gap-2 rounded-lg border border-gray-300 bg-white px-4 py-2.5 text-theme-sm font-medium text-gray-700 shadow-theme-xs hover:bg-gray-50 hover:text-gray-800 dark:border-gray-700 dark:bg-gray-800 dark:text-gray-400 dark:hover:bg-white/[0.03] dark:hover:text-gray-200">
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="stroke-current fill-white dark:fill-gray-800 size-4">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M6.75 15.75 3 12m0 0 3.75-3.75M3 12h18" />
                            </svg>

                            Go Back
                        </button>
                    </div>
                </div>
                <div class="grid grid-cols-12 gap-4 md:gap-6">
                    <div class="col-span-12 space-y-6 ">
                        <div class="grid grid-cols-2 gap-4 md:gap-6">
                            <div class="rounded-2xl border border-gray-200 bg-white p-5 dark:border-gray-800 dark:bg-white/[0.03] md:p-6">
                                <div class="flex items-end justify-between">
                                    <div>
                                        <span class="inline-flex items-center justify-center gap-1 rounded-full bg-brand-50 px-2.5 py-0.5 text-sm font-medium text-brand-500 dark:bg-brand-500/15 dark:text-brand-400">
                                            CPU Utilization
                                        </span>
                                        <h4 id="cpuUtilization" class="mt-2 text-title-sm font-bold text-gray-800 dark:text-white/90">
                                            {{ result?.cpuUtilization }} %
                                        </h4>
                                    </div>
                                </div>
                            </div>
                            <div class="rounded-2xl border border-gray-200 bg-white p-5 dark:border-gray-800 dark:bg-white/[0.03] md:p-6">
                                <div class="flex items-end justify-between">
                                    <div>
                                        <span class="inline-flex items-center justify-center gap-1 rounded-full bg-success-50 px-2.5 py-0.5 text-sm font-medium text-success-600 dark:bg-success-500/15 dark:text-success-500">
                                            Throughput
                                        </span>
                                        <h4 id="throughput" class="mt-2 text-title-sm font-bold text-gray-800 dark:text-white/90">
                                            {{ result?.throughput }}
                                        </h4>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="grid grid-cols-4 gap-4 md:gap-6">
                            <div class="rounded-2xl border border-gray-200 bg-white p-5 dark:border-gray-800 dark:bg-white/[0.03] md:p-6">
                                <div class="flex items-end justify-between">
                                    <div>
                                        <span class="inline-flex items-center justify-center gap-1 rounded-full bg-gray-100 px-2.5 py-0.5 text-sm font-medium text-gray-700 dark:bg-white/5 dark:text-white/80">
                                            Avg Turnaround Time
                                        </span>
                                        <h4 id="avgTurnaround" class="mt-2 text-title-sm font-bold text-gray-800 dark:text-white/90">
                                            {{ result?.avgTurnaround }}
                                        </h4>
                                    </div>
                                </div>
                            </div>
                            <div class="rounded-2xl border border-gray-200 bg-white p-5 dark:border-gray-800 dark:bg-white/[0.03] md:p-6">
                                <div class="flex items-end justify-between">
                                    <div>
                                        <span class="inline-flex items-center justify-center gap-1 rounded-full bg-gray-100 px-2.5 py-0.5 text-sm font-medium text-gray-700 dark:bg-white/5 dark:text-white/80">
                                            Avg Waiting Time
                                        </span>
                                        <h4 id="avgWaiting" class="mt-2 text-title-sm font-bold text-gray-800 dark:text-white/90">
                                            {{ result?.avgWaiting }}
                                        </h4>
                                    </div>
                                </div>
                            </div>
                            <div class="rounded-2xl border border-gray-200 bg-white p-5 dark:border-gray-800 dark:bg-white/[0.03] md:p-6">
                                <div class="flex items-end justify-between">
                                    <div>
                                        <span class="inline-flex items-center justify-center gap-1 rounded-full bg-gray-100 px-2.5 py-0.5 text-sm font-medium text-gray-700 dark:bg-white/5 dark:text-white/80">
                                            Avg Response Time
                                        </span>
                                        <h4 id="avgResponse" class="mt-2 text-title-sm font-bold text-gray-800 dark:text-white/90">
                                            {{ result?.avgResponse }}
                                        </h4>
                                    </div>
                                </div>
                            </div>
                            <div class="rounded-2xl border border-gray-200 bg-white p-5 dark:border-gray-800 dark:bg-white/[0.03] md:p-6">
                                <div class="flex items-end justify-between">
                                    <div>
                                        <span class="inline-flex items-center justify-center gap-1 rounded-full bg-gray-100 px-2.5 py-0.5 text-sm font-medium text-gray-700 dark:bg-white/5 dark:text-white/80">
                                            Total Time
                                        </span>
                                        <h4 id="totalTime" class="mt-2 text-title-sm font-bold text-gray-800 dark:text-white/90">
                                           {{ result?.totalTime }}
                                        </h4>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="mt-6 overflow-hidden rounded-2xl border border-gray-200 bg-white p-2  dark:border-gray-800 dark:bg-white/[0.03]" v-if="result && result?.ganttChart?.length > 0">
                <div class="flex my-2 flex-col gap-2 sm:flex-row sm:items-center sm:justify-between">
                    <div>
                        <h3 class="font-outfit text-lg font-semibold text-gray-800 dark:text-white/90">
                            Gantt Chart
                        </h3>
                    </div>
                </div>
                <div class="h-20 ">
                    <div class="overflow-x-auto scroll-small2 rounded-2xl h-full">
                        <div class="flex min-w-max h-16 rounded-2xl overflow-hidden">
                            <div class="w-25 shrink-0  bg-amber-400 text-center flex items-center justify-center flex-col gap-2" v-for="(segment, idx) in result?.ganttChart" :key="idx" 
                                :style="`background: ${colorMap[segment.pid]};min-width: ${(segment.end - segment.start) * 40}px;`">
                                <span class=" inline-flex items-center justify-center gap-1 rounded-full bg-gray-800 px-2.5 py-0.5 text-sm font-medium text-white dark:bg-white/15 dark:text-white" >
                                    {{ segment.pid }}
                                </span>
                                <h4 class="text-base font-bold text-white/90">
                                    {{segment.start}} - {{ segment.end }}
                                </h4>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="mt-6 overflow-hidden rounded-2xl border border-gray-200 bg-white p-5 dark:border-gray-800 dark:bg-white/[0.03] lg:p-6"  >
                <div class="flex flex-col gap-2 mb-4 sm:flex-row sm:items-center sm:justify-between">
                    <div>
                        <h3 class="font-outfit text-lg font-semibold text-gray-800 dark:text-white/90">
                            Process Detail
                        </h3>
                    </div>
                </div>
                <div class="rounded-2xl h-100 scroll-small bg-gray-100 border-gray-200 border dark:border-gray-800">
                    <div class="w-full rounded-2xl h-full bg-white px-5 pt-2 pb-2">
                        <div class="overflow-y-auto scroll-small w-full h-full pr-5 pb-5 rounded-2xl">
                            <div class="grid grid-cols-1 gap-4">
                                <div class="p-2 shadow-lg rounded-2xl flex bg-gray-100" v-for="(p, idx) in result?.processes" :key="idx">
                                    <div class="px-4 w-full flex items-center justify-between" >
                                        <div>
                                            <span class="text-theme-xs text-gray-500 dark:text-gray-400 sm:text-sm">ProcessID</span>
                                            <h4 class="mt-2 text-center text-base font-bold text-gray-800">{{p.pid}}</h4>
                                        </div>
                                        <div>
                                            <span class="text-sm text-gray-500 dark:text-gray-400">Arrival</span>
                                            <h4 class="mt-2 text-center text-base font-bold text-gray-800">{{p.arrival}}</h4>
                                        </div>
                                        <div>
                                            <span class="text-sm text-gray-500 dark:text-gray-400">Burst</span>
                                            <h4 class="mt-2 text-center text-base font-bold text-gray-800">{{p.burst}}</h4>
                                        </div>
                                        <div>
                                            <span class="text-sm text-gray-500 dark:text-gray-400">Priority</span>
                                            <h4 class="mt-2 text-center text-base font-bold text-gray-800">{{p.priority}}</h4>
                                        </div>
                                        <div>
                                            <span class="text-sm text-gray-500 dark:text-gray-400">Completion</span>
                                            <h4 class="mt-2 text-center text-base font-bold text-gray-800">{{p.completion}}</h4>
                                        </div>
                                        <div>
                                            <span class="text-sm text-gray-500 dark:text-gray-400">Turnaround</span>
                                            <h4 class="mt-2 text-center text-base font-bold text-gray-800">{{p.turnaround}}</h4>
                                        </div>
                                        <div>
                                            <span class="text-sm text-gray-500 dark:text-gray-400">Waiting</span>
                                            <h4 class="mt-2 text-center text-base font-bold text-gray-800">{{p.waiting}}</h4>
                                        </div>
                                        <div>
                                            <span class="text-sm text-gray-500 dark:text-gray-400">Response</span>
                                            <h4 class="mt-2 text-center text-base font-bold text-gray-800">{{p.response}}</h4>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </main>
</template>
<script>
import gsap from 'gsap'
export default {
    props: ['result', 'colorMap'],
    emits: ['goToPage'],
    mounted() {
        gsap.from("#cpuUtilization", {
            innerText: 0,
            duration: 1,
        });
        gsap.from("#throughput", {
            innerText: 0,
            duration: 1,
        });
        gsap.from("#avgTurnaround", {
            innerText: 0,
            duration: 1,
        });
        gsap.from("#avgWaiting", {
            innerText: 0,
            duration: 1,
        });
        gsap.from("#avgResponse", {
            innerText: 0,
            duration: 1,
        });
        gsap.from("#totalTime", {
            innerText: 0,
            duration: 1,
        });
    },
    methods: {
        downloadCSV(processes, filename = 'process_list.csv') {
            const processHeaders = Object.keys(processes[0]);
            const processRows = [
                '=== Process List ===',
                processHeaders.join(','),
                ...processes.map(obj => processHeaders.map(h => obj[h]).join(','))
            ];
            const summary = {
                cpuUtilization: this.result.cpuUtilization,
                throughput: this.result.throughput,
                avgTurnaround: this.result.avgTurnaround,
                avgWaiting: this.result.avgWaiting,
                avgResponse: this.result.avgResponse,
                totalTime: this.result.totalTime,
            }
            const summaryHeaders = Object.keys(summary);
            const summaryValues = Object.values(summary);
            const summaryRows = [
                '', 
                '=== Summary ===',
                summaryHeaders.join(','),
                summaryValues.join(',')
            ];
            const csvContent = [...processRows, ...summaryRows].join('\n');
            const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
            const url = URL.createObjectURL(blob);
            const link = document.createElement('a');
            link.href = url;
            link.download = filename;
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
        }
    },
}
</script>