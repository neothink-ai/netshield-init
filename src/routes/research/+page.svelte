<script>
    import { fade } from 'svelte/transition';
    import { initParticles } from '$lib/particles';
    import { onMount } from 'svelte';
    
    let particlesCanvas;
    let activeTab = 'dataset';
    const tabs = [
        { id: 'dataset', label: 'Dataset' },
        { id: 'graph', label: 'Graph Construction' },
        { id: 'model', label: 'Model Architecture' },
        { id: 'evaluation', label: 'Evaluation' }
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
                    <a href="/research" class="text-cyan-400">Research</a>
                    <a href="/simulation" class="text-white hover:text-cyan-400 transition-colors">Simulation</a>
                </div>
            </div>
        </div>
    </nav>

    <!-- Main Content -->
    <div class="max-w-7xl mx-auto px-6 py-12 relative">
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
        <div class="grid gap-8" in:fade={{duration: 200}}>
            {#if activeTab === 'dataset'}
                <div class="grid md:grid-cols-2 gap-8">
                    <div class="bg-slate-800/50 rounded-2xl p-6 backdrop-blur-sm border border-slate-700">
                        <h2 class="text-2xl font-bold text-cyan-400 mb-4 group-hover:text-cyan-300 transition-colors">  IoT-23 Dataset Overview</h2>
                        <p class="text-gray-300 mb-6 group-hover:text-gray-200 transition-colors">
                            Comprehensive collection of IoT network traffic data featuring both benign and malicious patterns.
                            Contains 23 scenarios covering various attack types and normal operations.
                        </p>
                        <div class="bg-slate-900/50 rounded-xl p-6 font-mono text-sm text-gray-300 border border-slate-800/50 group-hover:border-slate-700/50 transition-colors">
                            <pre class="group-hover:text-gray-200">Dataset Statistics:
├── Total Sessions: 325,000
├── Attack Types: 7
├── Benign Traffic: 76%
└── Malicious Traffic: 24%</pre>
                        </div>
                    </div>
                    
                    <div class="bg-slate-800/50 rounded-2xl p-6 backdrop-blur-sm border border-slate-700">
                        <h2 class="text-2xl font-bold text-cyan-400 mb-4">Data Distribution</h2>
                        <div class="aspect-square bg-slate-900/50 rounded-xl p-4 flex items-center justify-center">
                            <div class="text-gray-400">[Placeholder for Distribution Chart]</div>
                        </div>
                    </div>
                </div>
            {/if}

            {#if activeTab === 'graph'}
                <div class="grid md:grid-cols-2 gap-8">
                    <div class="bg-slate-800/50 rounded-2xl p-6 backdrop-blur-sm border border-slate-700">
                        <h2 class="text-2xl font-bold text-cyan-400 mb-4">Graph Construction Process</h2>
                        <p class="text-gray-300 mb-4">
                            Network traffic is transformed into a temporal graph structure where nodes represent devices
                            and edges represent network interactions.
                        </p>
                        <div class="bg-slate-900/50 rounded-xl p-4 flex items-center justify-center">
                            <div class="text-gray-400">[Placeholder for Graph Construction Diagram]</div>
                        </div>
                    </div>
                    
                    <div class="bg-slate-800/50 rounded-2xl p-6 backdrop-blur-sm border border-slate-700">
                        <h2 class="text-2xl font-bold text-cyan-400 mb-4">Feature Engineering</h2>
                        <div class="bg-slate-900/50 rounded-xl p-4 font-mono text-sm text-gray-300">
                            <pre>Node Features:
├── Device Type
├── Protocol Distribution
├── Traffic Volume
└── Connection States

Edge Features:
├── Protocol Type
├── Duration
├── Bytes Transferred
└── Port Numbers</pre>
                        </div>
                    </div>
                </div>
            {/if}

            {#if activeTab === 'model'}
                <div class="grid md:grid-cols-2 gap-8">
                    <div class="bg-slate-800/50 rounded-2xl p-6 backdrop-blur-sm border border-slate-700">
                        <h2 class="text-2xl font-bold text-cyan-400 mb-4">Model Architecture</h2>
                        <div class="bg-slate-900/50 rounded-xl p-4 flex items-center justify-center">
                            <div class="text-gray-400">[Placeholder for Architecture Diagram]</div>
                        </div>
                    </div>
                    
                    <div class="bg-slate-800/50 rounded-2xl p-6 backdrop-blur-sm border border-slate-700">
                        <h2 class="text-2xl font-bold text-cyan-400 mb-4">Implementation Details</h2>
                        <div class="bg-slate-900/50 rounded-xl p-4 font-mono text-sm text-gray-300 overflow-x-auto">
                            <pre>class GNNLayer(nn.Module):
    def __init__(self):
        super().__init__()
        self.gat = GATConv(
            in_channels=64,
            out_channels=64,
            heads=4
        )</pre>
                        </div>
                    </div>
                </div>
            {/if}

            {#if activeTab === 'evaluation'}
                <div class="grid md:grid-cols-2 gap-8">
                    <div class="bg-slate-800/50 rounded-2xl p-6 backdrop-blur-sm border border-slate-700">
                        <h2 class="text-2xl font-bold text-cyan-400 mb-4">Performance Metrics</h2>
                        <div class="bg-slate-900/50 rounded-xl p-4 flex items-center justify-center">
                            <div class="text-gray-400">[Placeholder for Performance Chart]</div>
                        </div>
                    </div>
                    
                    <div class="bg-slate-800/50 rounded-2xl p-6 backdrop-blur-sm border border-slate-700">
                        <h2 class="text-2xl font-bold text-cyan-400 mb-4">Comparative Analysis</h2>
                        <div class="space-y-4">
                            <div class="flex justify-between items-center">
                                <span class="text-gray-300">NetShield (Ours)</span>
                                <div class="w-48 h-2 bg-slate-700 rounded-full overflow-hidden">
                                    <div class="w-[92%] h-full bg-cyan-400"></div>
                                </div>
                                <span class="text-cyan-400">92%</span>
                            </div>
                            <div class="flex justify-between items-center">
                                <span class="text-gray-300">Baseline GCN</span>
                                <div class="w-48 h-2 bg-slate-700 rounded-full overflow-hidden">
                                    <div class="w-[78%] h-full bg-gray-400"></div>
                                </div>
                                <span class="text-gray-400">78%</span>
                            </div>
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
