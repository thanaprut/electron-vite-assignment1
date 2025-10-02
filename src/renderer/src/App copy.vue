<template>
    <div class="body_box">
        <div class="header_box dark:bg-gray-700 shadow-lg">
            <h1>Preemptive Priority</h1>
        </div>
        <div class="process_list bg-white rounded-xl shadow-lg p-6">
            <div class="flex justify-between items-center mb-4">
                <h2 class="text-xl font-semibold text-slate-800">Process Input</h2>
                <button @click="onReset()"
                    class="flex items-center gap-2 px-3 py-2 bg-slate-200 hover:bg-slate-300 rounded-lg transition-colors text-sm">
                    <svg
                        xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                        stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                        class="lucide lucide-refresh-cw w-4 h-4">
                        <path d="M3 12a9 9 0 0 1 9-9 9.75 9.75 0 0 1 6.74 2.74L21 8"></path>
                        <path d="M21 3v5h-5"></path>
                        <path d="M21 12a9 9 0 0 1-9 9 9.75 9.75 0 0 1-6.74-2.74L3 16"></path>
                        <path d="M8 16H3v5"></path>
                    </svg>Reset
                </button>
            </div>
            <div class="grid grid-cols-1 md:grid-cols-5 gap-2 mb-3">
                <input placeholder="PID" v-model="newProcess.pid"
                    class="px-3 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
                    type="text" >
                <input placeholder="Arrival" v-model="newProcess.arrival"
                    class="px-3 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
                    type="number" >
                <input placeholder="Burst" v-model="newProcess.burst"
                    class="px-3 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
                    type="number" >
                <input placeholder="Priority" v-model="newProcess.priority"
                    class="px-3 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
                    type="number">
                <button @click="onAddNewProcess()"
                    class="flex items-center justify-center gap-2 px-4 py-2 bg-blue-600 hover:bg-blue-700 text-white rounded-lg transition-colors">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                        stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                        class="lucide lucide-plus w-4 h-4">
                        <path d="M5 12h14"></path>
                        <path d="M12 5v14"></path>
                    </svg>
                    Add Process
                </button>
            </div>
            <div class="overflow-x-auto">
                <table class="w-full text-sm">
                    <thead class="bg-slate-100">
                        <tr>
                            <th class="px-3 py-2 text-left font-semibold text-slate-700">PID</th>
                            <th class="px-3 py-2 text-left font-semibold text-slate-700">Arrival</th>
                            <th class="px-3 py-2 text-left font-semibold text-slate-700">Burst</th>
                            <th class="px-3 py-2 text-left font-semibold text-slate-700">Priority</th>
                            <th class="px-3 py-2 text-left font-semibold text-slate-700">Action</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr class="border-b border-slate-200 hover:bg-slate-50" v-for="(process, index) in processList"
                            :key="index">
                            <td class="px-3 py-2 font-medium text-slate-800">{{ process.pid }}</td>
                            <td class="px-3 py-2 text-slate-600">{{ process.arrival }}</td>
                            <td class="px-3 py-2 text-slate-600">{{ process.burst }}</td>
                            <td class="px-3 py-2 text-slate-600">{{ process.priority }}</td>
                            <td class="px-3 py-2">
                                <button @click="deleteProcess(index)"
                                    class="cursor-pointer text-red-600 hover:text-red-800">
                                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                        fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                        stroke-linejoin="round" class="lucide lucide-trash2 w-4 h-4">
                                        <path d="M3 6h18"></path>
                                        <path d="M19 6v14c0 1-1 2-2 2H7c-1 0-2-1-2-2V6"></path>
                                        <path d="M8 6V4c0-1 1-2 2-2h4c1 0 2 1 2 2v2"></path>
                                        <line x1="10" x2="10" y1="11" y2="17"></line>
                                        <line x1="14" x2="14" y1="11" y2="17"></line>
                                    </svg>
                                </button>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
            <button @click="onCalculate()"
                class="w-full mt-4 flex items-center justify-center gap-2 px-4 py-3 bg-green-600 hover:bg-green-700 text-white rounded-lg font-semibold transition-colors"><svg
                    xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                    stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                    class="lucide lucide-play w-5 h-5">
                    <polygon points="6 3 20 12 6 21 6 3"></polygon>
                </svg>Run Scheduler
            </button>
        </div>
        <Transition name="fade">
            <div class="box bg-white rounded-xl shadow-lg p-6" v-if="result && result?.processes">
                <div class="mb-5">
                    <h2 class="text-xl font-semibold text-slate-800 mb-4">Process Details</h2>
                    <div class="overflow-x-auto">
                        <table class="w-full text-sm">
                            <thead class="bg-slate-100">
                            <tr>
                                <th class="px-4 py-3 text-left font-semibold text-slate-700">PID</th>
                                <th class="px-4 py-3 text-left font-semibold text-slate-700">Arrival</th>
                                <th class="px-4 py-3 text-left font-semibold text-slate-700">Burst</th>
                                <th class="px-4 py-3 text-left font-semibold text-slate-700">Priority</th>
                                <th class="px-4 py-3 text-left font-semibold text-slate-700">Completion</th>
                                <th class="px-4 py-3 text-left font-semibold text-slate-700">Turnaround</th>
                                <th class="px-4 py-3 text-left font-semibold text-slate-700">Waiting</th>
                                <th class="px-4 py-3 text-left font-semibold text-slate-700">Response</th>
                            </tr>
                            </thead>
                            <tbody>
                                <tr class="border-b border-slate-200 hover:bg-slate-50" v-for="(p, idx) in result?.processes" :key="idx">
                                    <td class="px-4 py-3 font-medium text-slate-800">{{p.pid}}</td>
                                    <td class="px-4 py-3 text-slate-600">{{p.arrival}}</td>
                                    <td class="px-4 py-3 text-slate-600">{{p.burst}}</td>
                                    <td class="px-4 py-3 text-slate-600">{{p.priority}}</td>
                                    <td class="px-4 py-3 text-slate-600">{{p.completion}}</td>
                                    <td class="px-4 py-3 text-slate-600">{{p.turnaround}}</td>
                                    <td class="px-4 py-3 text-slate-600">{{p.waiting}}</td>
                                    <td class="px-4 py-3 text-slate-600">{{p.response}}</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
                <h2 class="text-xl font-semibold text-slate-800 mb-4">Performance Metrics</h2>
                <div class="space-y-4">
                    <div class="grid grid-cols-2 gap-4">
                        <div class="bg-blue-50 p-4 rounded-lg">
                            <div class="text-sm text-blue-600 font-medium mb-1">CPU Utilization</div>
                            <div class="text-2xl font-bold text-blue-700" id="cpuUtilization">{{ result?.cpuUtilization }} %</div>
                        </div>
                        <div class="bg-green-50 p-4 rounded-lg">
                            <div class="text-sm text-green-600 font-medium mb-1">Throughput</div>
                            <div class="text-2xl font-bold text-green-700" id="throughput">{{ result?.throughput }}</div>
                        </div>
                    </div>
                    <div class="space-y-1">
                        <div class="flex justify-between p-3 bg-slate-50 rounded-lg">
                            <span class="text-slate-700 font-medium">Avg Turnaround Time</span>
                            <span class="text-slate-900 font-semibold" id="avgTurnaround">{{ result?.avgTurnaround }}</span>
                        </div>
                        <div class="flex justify-between p-3 bg-slate-50 rounded-lg">
                            <span class="text-slate-700 font-medium">Avg Waiting Time</span>
                            <span class="text-slate-900 font-semibold" id="avgWaiting">{{ result?.avgWaiting }}</span>
                        </div>
                        <div class="flex justify-between p-3 bg-slate-50 rounded-lg">
                            <span class="text-slate-700 font-medium">Avg Response Time</span>
                            <span class="text-slate-900 font-semibold" id="avgResponse">{{ result?.avgResponse }}</span>
                        </div>
                        <div class="flex justify-between p-3 bg-slate-50 rounded-lg">
                            <span class="text-slate-700 font-medium">Total Time</span>
                            <span class="text-slate-900 font-semibold" id="totalTime">{{ result?.totalTime }}</span>
                        </div>
                    </div>
                </div>
                <div class="mt-5" v-if="result && result?.ganttChart?.length > 0">
                    <h2 class="text-xl font-semibold text-slate-800 mb-4">Gantt Chart</h2>
                    <div class="overflow-x-auto">
                        <div class="flex min-w-max">
                            <div class="flex flex-col" v-for="(segment, idx) in result?.ganttChart" :key="idx">
                                <div class="border border-slate-300 px-4 py-3 text-center font-medium text-white" :style="`background: ${colorMap[segment.pid]};min-width: ${(segment.end - segment.start) * 40}px;`">
                                    {{ segment.pid }}
                                    <div class="text-xs text-white mt-1"><span>{{segment.start}}</span>-<span>{{ segment.end }}</span></div>
                                </div>
                                
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </Transition>
    </div>
    <div id="toast-bottom-right" class="fixed flex flex-col w-full max-w-xs p-4 space-x-4 rounded-lg shadow-sm right-5 bottom-5 " >
        <TransitionGroup name="fade">
            <div id="toast-danger" class="flex items-center w-full max-w-xs p-4 mb-4 text-gray-500 bg-white rounded-lg shadow-sm dark:text-gray-400 dark:bg-gray-800" role="alert" v-for="noti in notification" :key="noti">
                <div class="inline-flex items-center justify-center shrink-0 w-8 h-8 text-red-500 bg-red-100 rounded-lg dark:bg-red-800 dark:text-red-200">
                    <svg class="w-5 h-5" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor" viewBox="0 0 20 20">
                        <path d="M10 .5a9.5 9.5 0 1 0 9.5 9.5A9.51 9.51 0 0 0 10 .5Zm3.707 11.793a1 1 0 1 1-1.414 1.414L10 11.414l-2.293 2.293a1 1 0 0 1-1.414-1.414L8.586 10 6.293 7.707a1 1 0 0 1 1.414-1.414L10 8.586l2.293-2.293a1 1 0 0 1 1.414 1.414L11.414 10l2.293 2.293Z"/>
                    </svg>
                    <span class="sr-only">Error icon</span>
                </div>
                <div class="ms-3 text-sm font-normal">{{ noti }}</div>
            </div>
        </TransitionGroup>
    </div>
    
    <div style="width: 100%;display: flex;justify-content: center;">
        <footer class="bg-white rounded-lg shadow-sm m-4 dark:bg-gray-800" style="width: 62.5vw;">
            <div class="w-full mx-auto max-w-screen-xl p-4 md:flex md:items-center md:justify-center">
                <span class="text-sm text-gray-500 sm:text-center dark:text-gray-400">ธนพฤฒ วิบูลย์ภาณุเวช 1660904556</span>
            </div>
            <div class="w-full mx-auto max-w-screen-xl p-4 md:flex md:items-center md:justify-center">
                <span class="text-sm text-gray-500 sm:text-center dark:text-gray-400">ธนกร ปัญจสุนทร 1660901545</span>
            </div>
            <div class="w-full mx-auto max-w-screen-xl p-4 md:flex md:items-center md:justify-center">
                <span class="text-sm text-gray-500 sm:text-center dark:text-gray-400">ปรรณกฤติ ไพบูลย์กุลวงษ์ 1660904564</span>
            </div>
            <div class="w-full mx-auto max-w-screen-xl p-4 md:flex md:items-center md:justify-center">
                <span class="text-sm text-gray-500 sm:text-center dark:text-gray-400">ธนวินท์ วันหนุน 1660902550</span>
            </div>
        </footer>
    </div>
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
                { pid: 'P3', arrival: 2, burst: 5,  priority: 1 },
                { pid: 'P4', arrival: 3, burst: 3,  priority: 5 },
                { pid: 'P5', arrival: 3, burst: 15, priority: 4 },
                { pid: 'P6', arrival: 5, burst: 25, priority: 2 },
                { pid: 'P7', arrival: 6, burst: 10, priority: 1 },
                { pid: 'P8', arrival: 7, burst: 25, priority: 1 },
                { pid: 'P9', arrival: 7, burst: 5,  priority: 3 },
                { pid: 'P10', arrival: 9, burst: 10, priority: 3 }
            ],
            defaultList: [
                { pid: 'P1', arrival: 0, burst: 10, priority: 3 },
                { pid: 'P2', arrival: 1, burst: 20, priority: 2 },
                { pid: 'P3', arrival: 2, burst: 5,  priority: 1 },
                { pid: 'P4', arrival: 3, burst: 3,  priority: 5 },
                { pid: 'P5', arrival: 3, burst: 15, priority: 4 },
                { pid: 'P6', arrival: 5, burst: 25, priority: 2 },
                { pid: 'P7', arrival: 6, burst: 10, priority: 1 },
                { pid: 'P8', arrival: 7, burst: 25, priority: 1 },
                { pid: 'P9', arrival: 7, burst: 5,  priority: 3 },
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
