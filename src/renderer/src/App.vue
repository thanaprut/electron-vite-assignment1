<template>
    <Modal :modalActive="modalAddProcess">
        <div class="relative px-40 w-full max-w-2xl max-h-full">
            <div class="relative bg-white rounded-lg shadow-sm dark:bg-gray-700">
                <div
                    class="flex items-center justify-between p-4 md:p-5 border-b rounded-t dark:border-gray-600 border-gray-200">
                    <h3 class="text-xl font-semibold text-gray-900 dark:text-white">
                        Add Process
                    </h3>
                    <button @click="modalAddProcess = false" type="button"
                        class="text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm w-8 h-8 ms-auto inline-flex justify-center items-center dark:hover:bg-gray-600 dark:hover:text-white"
                        >
                        <svg class="w-3 h-3" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none"
                            viewBox="0 0 14 14">
                            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                d="m1 1 6 6m0 0 6 6M7 7l6-6M7 7l-6 6" />
                        </svg>
                        <span class="sr-only">Close modal</span>
                    </button>
                </div>
                <div class="p-4 md:p-5 space-y-4">
                    <div>
                        <label class="mb-1.5 block text-sm font-medium text-gray-700 dark:text-gray-400">
                            Process ID
                        </label>
                        <input type="text" v-model="newProcess.pid" 
                            class="dark:bg-dark-900 shadow-theme-xs focus:border-brand-300 focus:ring-brand-500/10 dark:focus:border-brand-800 h-11 w-full rounded-lg border border-gray-300 bg-transparent px-4 py-2.5 text-sm text-gray-800 placeholder:text-gray-400 focus:ring-3 focus:outline-hidden dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30" />
                    </div>
                    <div>
                        <label class="mb-1.5 block text-sm font-medium text-gray-700 dark:text-gray-400">
                            Arrival
                        </label>
                        <input type="number"  v-model="newProcess.arrival" 
                            class="dark:bg-dark-900 shadow-theme-xs focus:border-brand-300 focus:ring-brand-500/10 dark:focus:border-brand-800 h-11 w-full rounded-lg border border-gray-300 bg-transparent px-4 py-2.5 text-sm text-gray-800 placeholder:text-gray-400 focus:ring-3 focus:outline-hidden dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30" />
                    </div>
                    <div>
                        <label class="mb-1.5 block text-sm font-medium text-gray-700 dark:text-gray-400">
                            Burst Time
                        </label>
                        <input type="number" v-model="newProcess.burst" 
                            class="dark:bg-dark-900 shadow-theme-xs focus:border-brand-300 focus:ring-brand-500/10 dark:focus:border-brand-800 h-11 w-full rounded-lg border border-gray-300 bg-transparent px-4 py-2.5 text-sm text-gray-800 placeholder:text-gray-400 focus:ring-3 focus:outline-hidden dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30" />
                    </div>
                    <div>
                        <label class="mb-1.5 block text-sm font-medium text-gray-700 dark:text-gray-400">
                            Priority
                        </label>
                        <input type="number" v-model="newProcess.priority" 
                            class="dark:bg-dark-900 shadow-theme-xs focus:border-brand-300 focus:ring-brand-500/10 dark:focus:border-brand-800 h-11 w-full rounded-lg border border-gray-300 bg-transparent px-4 py-2.5 text-sm text-gray-800 placeholder:text-gray-400 focus:ring-3 focus:outline-hidden dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30" />
                    </div>
                </div>
                <div class="flex items-center p-4 md:p-5 border-t border-gray-200 rounded-b dark:border-gray-600">
                    <button 
                        @click="addNewProcess()"
                        type="button"
                        class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">
                        Done
                    </button>
                    <button type="button"
                        class="py-2.5 px-5 ms-3 text-sm font-medium text-gray-900 focus:outline-none bg-white rounded-lg border border-gray-200 hover:bg-gray-100 hover:text-blue-700 focus:z-10 focus:ring-4 focus:ring-gray-100 dark:focus:ring-gray-700 dark:bg-gray-800 dark:text-gray-400 dark:border-gray-600 dark:hover:text-white dark:hover:bg-gray-700">
                        Cancle
                    </button>
                </div>
            </div>
        </div>
    </Modal>

    <transition
        name="slide-fade"
        mode="out-in"
        >
        <div :key="page">
            <Main v-if="page === 'main'" :onClickAdd="onClickAdd" @file-uploaded="handleDataUpload"  @reset="onReset" @deleteProcess="deleteProcess" :onCalculate="onCalculate" >
                <TransitionGroup name="list">
                    <div class="p-2 shadow-lg rounded-2xl flex bg-gray-100" v-for="(process, index) in processList" :key="process.pid">
                        <div class="mx-4 flex items-center text-gray-800">
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
                                stroke-width="1.5" stroke="currentColor" class="size-6">
                                <path stroke-linecap="round" stroke-linejoin="round"
                                    d="M9.594 3.94c.09-.542.56-.94 1.11-.94h2.593c.55 0 1.02.398 1.11.94l.213 1.281c.063.374.313.686.645.87.074.04.147.083.22.127.325.196.72.257 1.075.124l1.217-.456a1.125 1.125 0 0 1 1.37.49l1.296 2.247a1.125 1.125 0 0 1-.26 1.431l-1.003.827c-.293.241-.438.613-.43.992a7.723 7.723 0 0 1 0 .255c-.008.378.137.75.43.991l1.004.827c.424.35.534.955.26 1.43l-1.298 2.247a1.125 1.125 0 0 1-1.369.491l-1.217-.456c-.355-.133-.75-.072-1.076.124a6.47 6.47 0 0 1-.22.128c-.331.183-.581.495-.644.869l-.213 1.281c-.09.543-.56.94-1.11.94h-2.594c-.55 0-1.019-.398-1.11-.94l-.213-1.281c-.062-.374-.312-.686-.644-.87a6.52 6.52 0 0 1-.22-.127c-.325-.196-.72-.257-1.076-.124l-1.217.456a1.125 1.125 0 0 1-1.369-.49l-1.297-2.247a1.125 1.125 0 0 1 .26-1.431l1.004-.827c.292-.24.437-.613.43-.991a6.932 6.932 0 0 1 0-.255c.007-.38-.138-.751-.43-.992l-1.004-.827a1.125 1.125 0 0 1-.26-1.43l1.297-2.247a1.125 1.125 0 0 1 1.37-.491l1.216.456c.356.133.751.072 1.076-.124.072-.044.146-.086.22-.128.332-.183.582-.495.644-.869l.214-1.28Z" />
                                <path stroke-linecap="round" stroke-linejoin="round"
                                    d="M15 12a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z" />
                            </svg>
                        </div>
                        <div class="px-4 w-full flex items-center justify-between">
                            <div>
                                <span class="text-theme-xs text-theme-xs text-gray-500 dark:text-gray-400 sm:text-sm">ProcessID</span>
                                <h4 class="mt-2 text-center text-base font-bold text-gray-800">{{ process.pid }}</h4>
                            </div>
                            <div>
                                <span class="text-sm text-gray-500 dark:text-gray-400">Arrival</span>
                                <h4 class="mt-2 text-center text-base font-bold text-gray-800">{{ process.arrival }}</h4>
                            </div>
                            <div>
                                <span class="text-sm text-gray-500 dark:text-gray-400">Burst</span>
                                <h4 class="mt-2 text-center text-base font-bold text-gray-800">{{ process.burst }}</h4>
                            </div>
                            <div>
                                <span class="text-sm text-gray-500 dark:text-gray-400">Priority</span>
                                <h4 class="mt-2 text-center text-base font-bold text-gray-800">{{ process.priority }}</h4>
                            </div>
                            <div @click="deleteProcess(index)">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="text-gray-800 hover:text-red-900 transition-all size-6">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="m14.74 9-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 0 1-2.244 2.077H8.084a2.25 2.25 0 0 1-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 0 0-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 0 1 3.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 0 0-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 0 0-7.5 0" />
                                </svg>
                            </div>
                        </div>
                    </div>
                </TransitionGroup>
            </Main>
            <Detail v-if="page === 'detail'" @goToPage="gotoPage"  :result="result" :colorMap="colorMap" />
        </div>
    </transition>
</template>
<script>

import Modal from './components/Modal.vue';
import Main from './pages/main.vue';
import Detail from './pages/detail.vue';


export default {
    name: "MainContainer",
    components: { Modal, Main, Detail },
    data() {
        return {
            modalAddProcess: false,
            page: 'main',
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
        handleDataUpload(data) {
            this.processList = []
            this.processList = data
        },
        onClickAdd() {
            this.modalAddProcess = ! this.modalAddProcess
        },
        gotoPage(page) {
            this.page = page
        },
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
        addNewProcess() {
            if (!this.newProcess.pid || !this.newProcess.arrival || !this.newProcess.burst || !this.newProcess.priority) {
                console.log('fill')
                return;
            }
            this.modalAddProcess = false
            this.processList.push(this.newProcess)
            this.newProcess = {
                pid: undefined,
                arrival: undefined,
                burst: undefined,
                priority: undefined,
            }
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
            this.page = 'detail'

            // setTimeout(() => {
            //     gsap.from("#cpuUtilization", {
            //         innerText: 0,
            //         duration: 2,
            //     });
            //     gsap.from("#throughput", {
            //         innerText: 0,
            //         duration: 2,
            //     });
            //     gsap.from("#avgTurnaround", {
            //         innerText: 0,
            //         duration: 2,
            //     });
            //     gsap.from("#avgWaiting", {
            //         innerText: 0,
            //         duration: 2,
            //     });
            //     gsap.from("#avgResponse", {
            //         innerText: 0,
            //         duration: 2,
            //     });
            //     gsap.from("#totalTime", {
            //         innerText: 0,
            //         duration: 2,
            //     });
            // }, 1000);
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
