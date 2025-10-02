<template>
    <main>
        <div class="p-4 mx-auto max-w-(--breakpoint-2xl) md:p-6">
            <div class="rounded-2xl border border-gray-200 bg-white p-5 dark:border-gray-800 dark:bg-white/[0.03] lg:p-6">
                <div class="flex flex-col gap-2 mb-4 sm:flex-row sm:items-center sm:justify-between">
                    <div>
                        <h3 class="text-lg font-semibold text-gray-800 dark:text-white/90">
                            Process Input
                        </h3>
                    </div>
                    <div class="flex items-center gap-3">

                    <button class="inline-flex items-center gap-2 px-4 py-3 text-sm font-medium text-white text-theme-sm font-medium text-gray-700 transition rounded-lg bg-brand-500 shadow-theme-xs hover:bg-brand-600">
                        Add
                    </button>
                    <button
                        class="inline-flex items-center gap-2 rounded-lg border border-gray-300 bg-white px-4 py-2.5 text-theme-sm font-medium text-gray-700 shadow-theme-xs hover:bg-gray-50 hover:text-gray-800 dark:border-gray-700 dark:bg-gray-800 dark:text-gray-400 dark:hover:bg-white/[0.03] dark:hover:text-gray-200">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="stroke-current fill-white dark:fill-gray-800 size-4">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M16.023 9.348h4.992v-.001M2.985 19.644v-4.992m0 0h4.992m-4.993 0 3.181 3.183a8.25 8.25 0 0 0 13.803-3.7M4.031 9.865a8.25 8.25 0 0 1 13.803-3.7l3.181 3.182m0-4.991v4.99" />
                        </svg>
                        Reset
                    </button>
                </div>
                </div>
                <div class="p-5 border-t border-gray-100 dark:border-gray-800 sm:p-6">
                    <div class="overflow-hidden rounded-xl border border-gray-200 bg-white dark:border-gray-800 dark:bg-white/[0.03]">
                        <div class="max-w-full overflow-x-auto">
                            <table class="min-w-full">
                                <thead>
                                    <tr class="border-b border-gray-100 dark:border-gray-800">
                                        <th class="px-5 py-3 sm:px-6">
                                            <div class="flex items-center">
                                                <p class="font-medium text-gray-500 text-theme-xs dark:text-gray-400">
                                                    PID
                                                </p>
                                            </div>
                                        </th>
                                        <th class="px-5 py-3 sm:px-6">
                                            <div class="flex items-center">
                                                <p class="font-medium text-gray-500 text-theme-xs dark:text-gray-400">
                                                    Arrival
                                                </p>
                                            </div>
                                        </th>
                                        <th class="px-5 py-3 sm:px-6">
                                            <div class="flex items-center">
                                                <p class="font-medium text-gray-500 text-theme-xs dark:text-gray-400">
                                                    Burst
                                                </p>
                                            </div>
                                        </th>
                                        <th class="px-5 py-3 sm:px-6">
                                            <div class="flex items-center">
                                                <p class="font-medium text-gray-500 text-theme-xs dark:text-gray-400">
                                                    Priority
                                                </p>
                                            </div>
                                        </th>
                                        <th class="px-5 py-3 sm:px-6">
                                            <div class="flex items-center">
                                                <p class="font-medium text-gray-500 text-theme-xs dark:text-gray-400">
                                                    Action
                                                </p>
                                            </div>
                                        </th>
                                    </tr>
                                </thead>
                                <tbody class="divide-y divide-gray-100 dark:divide-gray-800">
                                    <tr>
                                        <td class="px-5 py-4 sm:px-6">
                                            <div class="flex items-center">
                                                <p class="text-gray-500 text-theme-sm dark:text-gray-400">
                                                    P1
                                                </p>
                                            </div>
                                        </td>
                                        <td class="px-5 py-4 sm:px-6">
                                            <div class="flex items-center">
                                                <p class="text-gray-500 text-theme-sm dark:text-gray-400">
                                                    1
                                                </p>
                                            </div>
                                        </td>
                                        <td class="px-5 py-4 sm:px-6">
                                            <div class="flex items-center">
                                                <p class="text-gray-500 text-theme-sm dark:text-gray-400">
                                                    2
                                                </p>
                                            </div>
                                        </td>
                                        <td class="px-5 py-4 sm:px-6">
                                            <div class="flex items-center">
                                                <p class="text-gray-500 text-theme-sm dark:text-gray-400">
                                                    3
                                                </p>
                                            </div>
                                        </td>
                                        <td class="px-5 py-4 sm:px-6">
                                            <div class="flex items-center">
                                                <p class="text-gray-500 text-theme-sm dark:text-gray-400">
                                                    4
                                                </p>
                                            </div>
                                        </td>
                                    </tr>

                                </tbody>
                            </table>
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
    name: "MainContainer",
    data() {
        return {
            result: [],
            processList: [
                { pid: 'P1', arrival: 0, burst: 10, priority: 3 },
                { pid: 'P2', arrival: 1, burst: 20, priority: 2 },
                { pid: 'P3', arrival: 2, burst: 5, priority: 1 },
                { pid: 'P4', arrival: 3, burst: 3, priority: 5 },
                { pid: 'P5', arrival: 3, burst: 15, priority: 4 },
                { pid: 'P6', arrival: 5, burst: 25, priority: 2 },
                { pid: 'P7', arrival: 6, burst: 10, priority: 1 },
                { pid: 'P8', arrival: 7, burst: 25, priority: 1 },
                { pid: 'P9', arrival: 7, burst: 5, priority: 3 },
                { pid: 'P10', arrival: 9, burst: 10, priority: 3 }
            ],
            defaultList: [
                { pid: 'P1', arrival: 0, burst: 10, priority: 3 },
                { pid: 'P2', arrival: 1, burst: 20, priority: 2 },
                { pid: 'P3', arrival: 2, burst: 5, priority: 1 },
                { pid: 'P4', arrival: 3, burst: 3, priority: 5 },
                { pid: 'P5', arrival: 3, burst: 15, priority: 4 },
                { pid: 'P6', arrival: 5, burst: 25, priority: 2 },
                { pid: 'P7', arrival: 6, burst: 10, priority: 1 },
                { pid: 'P8', arrival: 7, burst: 25, priority: 1 },
                { pid: 'P9', arrival: 7, burst: 5, priority: 3 },
                { pid: 'P10', arrival: 9, burst: 10, priority: 3 }
            ],
            newProcess: {
                pid: undefined,
                arrival: undefined,
                burst: undefined,
                priority: undefined,
            },
            colorMap: {},
            notification: [],
        }
    },
    mounted() {

    },
    methods: {
        addNoti(text) {
            this.notification.push(text)
            setTimeout(() => {
                this.notification.shift();
            }, 2000);
        },
        getGanttColor() {
            const colors = ['#3b82f6', '#ef4444', '#10b981', '#f59e0b', '#8b5cf6', '#ec4899', '#06b6d4', '#84cc16', '#f97316', '#6366f1'];
            const colorMap = {};
            let colorIndex = 0;
            this.result.ganttChart.forEach(chart => {
                const pid = chart.pid
                console.log(colorMap[pid], pid, colorIndex)
                if (pid !== "Idle" && !colorMap[pid]) {
                    colorMap[pid] = colors[colorIndex % colors.length];
                    colorIndex++;
                }
            });
            return colorMap;
        },
        onAddNewProcess() {
            if (!this.newProcess.pid || !this.newProcess.arrival || !this.newProcess.burst || !this.newProcess.priority) {
                alert('Please fill all fields');
                return;
            }
            this.processList.push(this.newProcess)
        },
        deleteProcess(processId) {
            this.processList.splice(processId, 1)
        },
        onCalculate() {
            if (this.processList.length <= 0) {
                this.addNoti("กรุณาใส่ ข้อมูล Process ให้ครบถ้วน")
                return
            }
            this.result = this.preemptivePriorityScheduling(this.processList)
            this.colorMap = this.getGanttColor()

            setTimeout(() => {
                gsap.from("#cpuUtilization", {
                    innerText: 0,
                    duration: 2,
                });
                gsap.from("#throughput", {
                    innerText: 0,
                    duration: 2,
                });
                gsap.from("#avgTurnaround", {
                    innerText: 0,
                    duration: 2,
                });
                gsap.from("#avgWaiting", {
                    innerText: 0,
                    duration: 2,
                });
                gsap.from("#avgResponse", {
                    innerText: 0,
                    duration: 2,
                });
                gsap.from("#totalTime", {
                    innerText: 0,
                    duration: 2,
                });
            }, 1000);
        },
        onReset() {
            this.result = []
            this.processList = JSON.parse(JSON.stringify(this.defaultList))

        },
        preemptivePriorityScheduling(process) {
            const processList = process.map(p => ({
                ...p,
                remaining: p.burst,
                completion: 0,
                turnaround: 0,
                waiting: 0,
                startTime: -1,
                response: 0
            }));

            let time = 0;
            let completed = 0;
            const n = processList.length;
            const ganttChart = [];
            const timeline = [];
            while (completed < n) {
                const available = processList.filter(p => p.arrival <= time && p.remaining > 0);

                if (available.length > 0) {
                    const current = available.reduce((min, p) =>
                        p.priority < min.priority ? p : min
                    );

                    ganttChart.push(current.pid);

                    if (current.startTime === -1) {
                        current.startTime = time;
                    }

                    current.remaining -= 1;
                    time += 1;

                    if (current.remaining === 0) {
                        current.completion = time;
                        current.turnaround = current.completion - current.arrival;
                        current.waiting = current.turnaround - current.burst;
                        current.response = current.startTime - current.arrival;
                        completed += 1;
                    }
                } else {
                    ganttChart.push('Idle');
                    time += 1;
                }
            }
            const compressed = [];
            let i = 0;
            while (i < ganttChart.length) {
                const pid = ganttChart[i];
                const start = i;
                while (i < ganttChart.length && ganttChart[i] === pid) {
                    i++;
                }
                compressed.push({ pid, start, end: i });
            }
            const cpuBusyTime = ganttChart.filter(pid => pid !== 'Idle').length;
            const cpuUtilization = (cpuBusyTime / time) * 100;
            const throughput = n / time;
            const avgTurnaround = processList.reduce((sum, p) => sum + p.turnaround, 0) / n;
            const avgWaiting = processList.reduce((sum, p) => sum + p.waiting, 0) / n;
            const avgResponse = processList.reduce((sum, p) => sum + p.response, 0) / n;

            return {
                processes: processList,
                ganttChart: compressed,
                totalTime: time,
                cpuUtilization,
                throughput,
                avgTurnaround,
                avgWaiting,
                avgResponse
            };
        },
    },
};
</script>
