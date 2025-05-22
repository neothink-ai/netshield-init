<script lang="ts">    import { onMount } from 'svelte';
    import { simulationStore } from '$lib/stores/simulation-store';
    import { initParticles } from '$lib/particles';
    
    let sourceIP = '';
    let destIP = '';
    let protocol = '';
    let packetLength = 0;
    let interarrivalTime = 0;
    let particlesCanvas;

    function handleSubmit() {
        simulationStore.addPacket(sourceIP, destIP, protocol, packetLength, interarrivalTime);
    }

    function resetGraph() {
        simulationStore.reset();
    }

    onMount(() => {
        const cleanupParticles = initParticles(particlesCanvas);
        return () => {
            cleanupParticles();
        };
    });
</script>

<nav class="fixed w-full bg-slate-900/90 backdrop-blur-sm z-50 px-6 py-4">
    <div class="max-w-7xl mx-auto flex justify-between items-center">
        <div class="flex items-center space-x-2">
            <div class="w-8 h-8 rounded-full bg-cyan-500/20 flex items-center justify-center">
                <div class="w-6 h-6 rounded-full bg-cyan-400/40 flex items-center justify-center">
                    <div class="w-4 h-4 rounded-full bg-cyan-300"></div>
                </div>
            </div>
            <span class="text-cyan-400 font-bold text-xl">NetShield</span>
        </div>
        <div class="space-x-8">
            <a href="/research" class="text-white hover:text-cyan-400 transition-colors duration-300">Research</a>
            <a href="/analytics" class="text-white hover:text-cyan-400 transition-colors duration-300">Analytics</a>
            <a href="/simulation" class="text-white hover:text-cyan-400 transition-colors duration-300">Simulation</a>
        </div>
    </div>
</nav>

<main class="min-h-screen bg-slate-900 text-white relative overflow-hidden">
    <canvas
        bind:this={particlesCanvas}
        class="absolute inset-0 w-full h-full opacity-30"
    ></canvas>
    
    <div class="relative pt-32 pb-20 px-6">
        <div class="max-w-7xl mx-auto">
            <div class="mb-12">
                <h1 class="text-4xl md:text-5xl font-bold mb-6">
                    Network <span class="text-cyan-400">Simulation</span>
                    <div class="relative w-16 h-1 bg-cyan-400 mt-4 overflow-hidden">
                        <div class="absolute inset-0 bg-cyan-300 animate-pulse"></div>
                    </div>
                </h1>
                <p class="text-gray-400 text-lg max-w-2xl">
                    Configure and visualize network traffic patterns through an interactive graph-based simulation.
                </p>
            </div>

            <div class="grid lg:grid-cols-2 gap-12 items-start">
                <div class="bg-slate-800/50 backdrop-blur-sm border border-slate-700 rounded-2xl p-8">
                    <form on:submit|preventDefault={handleSubmit} class="space-y-6">
                        <div class="grid grid-cols-1 gap-6 sm:grid-cols-2">
                            <div>
                                <label for="sourceIP" class="block text-sm font-medium text-gray-300">Source IP</label>
                                <input 
                                    type="text" 
                                    id="sourceIP" 
                                    bind:value={sourceIP}
                                    placeholder="192.168.1.1"
                                    pattern="^(\d{1,3}\.){3}\d{1,3}$"
                                    title="Please enter a valid IP address (e.g., 192.168.1.1)"
                                    class="mt-1 block w-full bg-slate-900/50 border border-slate-700 rounded-xl
                                    text-gray-300 placeholder-gray-500 focus:border-cyan-400 focus:ring-cyan-400/50
                                    shadow-sm transition-colors duration-200"
                                    required
                                />
                            </div>

                            <div>
                                <label for="destIP" class="block text-sm font-medium text-gray-300">Destination IP</label>
                                <input 
                                    type="text" 
                                    id="destIP" 
                                    bind:value={destIP}
                                    placeholder="192.168.1.2"
                                    pattern="^(\d{1,3}\.){3}\d{1,3}$"
                                    title="Please enter a valid IP address (e.g., 192.168.1.1)"
                                    class="mt-1 block w-full bg-slate-900/50 border border-slate-700 rounded-xl
                                    text-gray-300 placeholder-gray-500 focus:border-cyan-400 focus:ring-cyan-400/50
                                    shadow-sm transition-colors duration-200"
                                    required
                                />
                            </div>
                        </div>

                        <div>
                            <label for="protocol" class="block text-sm font-medium text-gray-300">Protocol</label>
                            <select 
                                id="protocol" 
                                bind:value={protocol}
                                class="mt-1 block w-full bg-slate-900/50 border border-slate-700 rounded-xl
                                text-gray-300 focus:border-cyan-400 focus:ring-cyan-400/50
                                shadow-sm transition-colors duration-200"
                                required
                            >
                                <option value="">Select Protocol</option>
                                <option value="TCP">TCP</option>
                                <option value="UDP">UDP</option>
                                <option value="ICMP">ICMP</option>
                            </select>
                        </div>

                        <div class="grid grid-cols-1 gap-6 sm:grid-cols-2">
                            <div>
                                <label for="packetLength" class="block text-sm font-medium text-gray-300">Packet Length (bytes)</label>
                                <input 
                                    type="number" 
                                    id="packetLength" 
                                    bind:value={packetLength}
                                    min="0"
                                    max="65535"
                                    class="mt-1 block w-full bg-slate-900/50 border border-slate-700 rounded-xl
                                    text-gray-300 placeholder-gray-500 focus:border-cyan-400 focus:ring-cyan-400/50
                                    shadow-sm transition-colors duration-200"
                                    required
                                />
                            </div>

                            <div>
                                <label for="interarrivalTime" class="block text-sm font-medium text-gray-300">Interarrival Time (ms)</label>
                                <input 
                                    type="number" 
                                    id="interarrivalTime" 
                                    bind:value={interarrivalTime}
                                    min="0"
                                    class="mt-1 block w-full bg-slate-900/50 border border-slate-700 rounded-xl
                                    text-gray-300 placeholder-gray-500 focus:border-cyan-400 focus:ring-cyan-400/50
                                    shadow-sm transition-colors duration-200"
                                    required
                                />
                            </div>
                        </div>

                        <div class="flex gap-4 pt-4">
                            <button 
                                type="submit" 
                                class="flex-1 px-6 py-3 bg-slate-800 text-cyan-400 border border-cyan-400
                                rounded-xl hover:bg-cyan-400 hover:text-slate-900 transition-all duration-300
                                shadow-lg shadow-cyan-400/20 hover:shadow-cyan-400/40"
                            >
                                Build Graph
                            </button>
                            <button 
                                type="button" 
                                on:click={resetGraph}
                                class="flex-1 px-6 py-3 bg-transparent text-white border border-white/20
                                rounded-xl hover:border-white/40 transition-all duration-300"
                            >
                                Reset Graph
                            </button>
                        </div>
                    </form>
                </div>                <div class="bg-slate-800/50 backdrop-blur-sm border border-slate-700 rounded-2xl p-8 min-h-[400px]">
                    {#if $simulationStore.nodes.length > 0}
                        <div class="space-y-6">
                            <div class="bg-slate-900/50 rounded-xl p-4">
                                <h3 class="text-lg font-semibold text-cyan-400 mb-3">Network Graph</h3>
                                <div class="grid grid-cols-2 gap-6">
                                    <div>
                                        <h4 class="text-sm font-medium text-gray-300 mb-2">Nodes</h4>
                                        <div class="space-y-2">
                                            {#each $simulationStore.nodes as node}
                                                <div class="flex items-center bg-slate-800/50 rounded-lg p-2">
                                                    <div class="w-3 h-3 rounded-full bg-cyan-400 mr-2"></div>
                                                    <span class="text-sm text-gray-300 font-mono">{node.id}</span>
                                                </div>
                                            {/each}
                                        </div>
                                    </div>
                                    <div>
                                        <h4 class="text-sm font-medium text-gray-300 mb-2">Edges</h4>
                                        <div class="space-y-2">
                                            {#each $simulationStore.edges as edge}
                                                <div class="bg-slate-800/50 rounded-lg p-2">
                                                    <div class="flex items-center text-sm text-gray-300 font-mono mb-1">
                                                        <span>{edge.from}</span>
                                                        <svg class="w-4 h-4 mx-2 text-cyan-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3"/>
                                                        </svg>
                                                        <span>{edge.to}</span>
                                                    </div>
                                                    <div class="text-xs text-gray-400">
                                                        {edge.protocol} | {edge.packetLength} bytes | {edge.interarrivalTime}ms
                                                    </div>
                                                </div>
                                            {/each}
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="bg-slate-900/90 rounded-xl p-4">
                                <h3 class="text-sm font-medium text-gray-300 mb-2">Raw Data</h3>
                                <div class="text-sm font-mono text-gray-400 overflow-x-auto">
                                    <pre class="whitespace-pre-wrap">{JSON.stringify($simulationStore, null, 2)}</pre>
                                </div>
                            </div>
                        </div>
                    {:else}
                        <div class="flex flex-col items-center justify-center h-full text-center">
                            <div class="text-cyan-400 mb-4">
                                <svg class="w-12 h-12" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M9 20l-5.447-2.724A1 1 0 013 16.382V5.618a1 1 0 011.447-.894L9 7m0 13l6-3m-6 3V7m6 10l4.553 2.276A1 1 0 0021 18.382V7.618a1 1 0 00-.553-.894L15 4m0 13V4m0 0L9 7"/>
                                </svg>
                            </div>
                            <h3 class="text-lg font-semibold text-gray-300 mb-2">No Network Data</h3>
                            <p class="text-gray-400">Add network packets using the form to visualize the graph</p>
                        </div>
                    {/if}
                </div>
            </div>
        </div>
    </div>
</main>

<style>
    :global(input[type="number"]::-webkit-inner-spin-button),
    :global(input[type="number"]::-webkit-outer-spin-button) {
        -webkit-appearance: none;
        margin: 0;
    }
    :global(input[type="number"]) {
        -moz-appearance: textfield;
    }
</style>