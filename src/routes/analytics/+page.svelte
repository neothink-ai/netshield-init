<script>
    import { onMount } from 'svelte';
    import { initParticles } from '$lib/particles';
    
    let particlesCanvas;
    let activeTab = 'traffic';
    const tabs = [
        { id: 'traffic', label: 'Traffic Distribution' },
        { id: 'patterns', label: 'Attack Patterns' },
        { id: 'protocols', label: 'Protocol Analysis' },
        { id: 'anomalies', label: 'Anomaly Detection' }
    ];

    onMount(() => {
        const cleanup = initParticles(particlesCanvas);
        return cleanup;
    });

    function setActiveTab(tabId) {
        activeTab = tabId;
    }
</script>

<div class="min-h-screen bg-slate-900 text-white relative overflow-hidden">
    <canvas
        class="absolute inset-0 w-full h-full opacity-20 pointer-events-none"
        bind:this={particlesCanvas}
    ></canvas>

    <!-- Navigation -->
    <nav class="sticky top-0 z-50 bg-slate-900/90 backdrop-blur-sm border-b border-slate-800/50">
        <div class="max-w-7xl mx-auto px-6 py-4">
            <div class="flex items-center justify-between">
                <div class="flex items-center space-x-2">
                    <div class="w-8 h-8 rounded-full bg-cyan-500/20 flex items-center justify-center">
                        <div class="w-6 h-6 rounded-full bg-cyan-400/40 flex items-center justify-center">
                            <div class="w-4 h-4 rounded-full bg-cyan-300"></div>
                        </div>
                    </div>
                    <a href="/" class="text-cyan-400 font-bold text-xl">NetShield</a>
                </div>
                <div class="space-x-8">
                    <a href="/" class="text-white hover:text-cyan-400 transition-colors">Home</a>
                    <a href="/research" class="text-white hover:text-cyan-400 transition-colors">Research</a>
                    <a href="/analytics" class="text-cyan-400">Analytics</a>
                    <a href="/simulation" class="text-white hover:text-cyan-400 transition-colors">Simulation</a>
                </div>
            </div>
        </div>
    </nav>

    <!-- Main Content -->
    <div class="max-w-7xl mx-auto px-6 py-12">
        <h1 class="text-4xl font-bold mb-8">
            Network Traffic <span class="text-cyan-400">Analytics</span>
        </h1>

        <!-- Tabs -->
        <div class="flex flex-wrap gap-2 mb-12">
            <div class="w-full flex gap-2 p-1 bg-slate-800/30 backdrop-blur-sm rounded-2xl">
                {#each tabs as tab}
                    <button
                        class="flex-1 px-6 py-4 rounded-xl text-sm font-medium transition-all duration-300
                        {activeTab === tab.id 
                            ? 'bg-cyan-400 text-slate-900 shadow-lg shadow-cyan-400/20' 
                            : 'text-gray-400 hover:text-white hover:bg-slate-700/50'}"
                        on:click={() => setActiveTab(tab.id)}
                    >
                        {tab.label}
                    </button>
                {/each}
            </div>
        </div>

        <!-- Content -->
        <div class="grid gap-8">
            {#if activeTab === 'traffic'}
                <div class="grid md:grid-cols-2 gap-8">
                    <div class="bg-slate-800/50 rounded-2xl p-6 backdrop-blur-sm border border-slate-700">
                        <h2 class="text-2xl font-bold text-cyan-400 mb-4">Traffic Distribution</h2>
                        <div class="aspect-square bg-slate-900/50 rounded-xl p-4 flex items-center justify-center">
                            <div class="text-gray-400">[Placeholder for Traffic Distribution Chart]</div>
                        </div>
                    </div>
                    
                    <div class="bg-slate-800/50 rounded-2xl p-6 backdrop-blur-sm border border-slate-700">
                        <h2 class="text-2xl font-bold text-cyan-400 mb-4">Traffic Metrics</h2>
                        <div class="space-y-4">
                            <div class="p-4 bg-slate-900/50 rounded-xl">
                                <div class="flex justify-between items-center mb-2">
                                    <span class="text-gray-300">Benign Traffic</span>
                                    <span class="text-cyan-400">76%</span>
                                </div>
                                <div class="w-full h-2 bg-slate-700 rounded-full overflow-hidden">
                                    <div class="w-[76%] h-full bg-cyan-400"></div>
                                </div>
                            </div>
                            <div class="p-4 bg-slate-900/50 rounded-xl">
                                <div class="flex justify-between items-center mb-2">
                                    <span class="text-gray-300">Malicious Traffic</span>
                                    <span class="text-red-400">24%</span>
                                </div>
                                <div class="w-full h-2 bg-slate-700 rounded-full overflow-hidden">
                                    <div class="w-[24%] h-full bg-red-400"></div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            {/if}

            {#if activeTab === 'patterns'}
                <div class="grid md:grid-cols-2 gap-8">
                    <div class="bg-slate-800/50 rounded-2xl p-6 backdrop-blur-sm border border-slate-700">
                        <h2 class="text-2xl font-bold text-cyan-400 mb-4">Attack Pattern Distribution</h2>
                        <div class="aspect-square bg-slate-900/50 rounded-xl p-4 flex items-center justify-center">
                            <div class="text-gray-400">[Placeholder for Attack Patterns Chart]</div>
                        </div>
                    </div>
                    
                    <div class="bg-slate-800/50 rounded-2xl p-6 backdrop-blur-sm border border-slate-700">
                        <h2 class="text-2xl font-bold text-cyan-400 mb-4">Common Attack Vectors</h2>
                        <div class="space-y-4">
                            <!-- Add attack vector statistics here -->
                        </div>
                    </div>
                </div>
            {/if}

            {#if activeTab === 'protocols'}
                <div class="grid md:grid-cols-2 gap-8">
                    <div class="bg-slate-800/50 rounded-2xl p-6 backdrop-blur-sm border border-slate-700">
                        <h2 class="text-2xl font-bold text-cyan-400 mb-4">Protocol Distribution</h2>
                        <div class="aspect-square bg-slate-900/50 rounded-xl p-4 flex items-center justify-center">
                            <div class="text-gray-400">[Placeholder for Protocol Distribution Chart]</div>
                        </div>
                    </div>
                </div>
            {/if}

            {#if activeTab === 'anomalies'}
                <div class="grid md:grid-cols-2 gap-8">
                    <div class="bg-slate-800/50 rounded-2xl p-6 backdrop-blur-sm border border-slate-700">
                        <h2 class="text-2xl font-bold text-cyan-400 mb-4">Anomaly Detection Results</h2>
                        <div class="aspect-square bg-slate-900/50 rounded-xl p-4 flex items-center justify-center">
                            <div class="text-gray-400">[Placeholder for Anomaly Detection Chart]</div>
                        </div>
                    </div>
                </div>
            {/if}
        </div>
    </div>
</div>

<style>
    :global(html) {
        scroll-behavior: smooth;
    }
</style>
