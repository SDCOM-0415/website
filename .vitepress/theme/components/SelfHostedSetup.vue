<template>
  <div class="self-hosted-setup-section">
    <div class="columns-container">

      <div class="image-column">
        <img src="/images/quick_setup.png" alt="自托管安装示意图" style="max-width: 100%; height: auto; border-radius: 0.5rem; box-shadow: 0 4px 6px -1px rgba(0,0,0,0.1), 0 2px 4px -1px rgba(0,0,0,0.06);">
      </div>

      <div class="text-content-column">
        <div class="method-card">
          <div style="display: flex; align-items: center; margin-bottom: 0.75rem;">
            <h3 style="font-size: 1.125rem; font-weight: 600; margin-top: 0;">方法 1: 使用脚本一键安装</h3>
          </div>
          <div style="display: flex; align-items: center; gap: 0.5rem; margin-bottom: 0.5rem;">
            <pre><code>{{ command1Text }}</code></pre>
            <button @click="triggerCopy(command1Text, 'cmd1')" :style="copyIconButtonBaseStyle" title="复制命令" class="copy-button">
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" :style="copyIconSvgStyle"><path d="M16 1H4c-1.1 0-2 .9-2 2v14h2V3h12V1zm3 4H8c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h11c1.1 0 2-.9 2-2V7c0-1.1-.9-2-2-2zm0 16H8V7h11v14z"/></svg>
            </button>
          </div>
          <div v-if="isSuccess && lastCopiedId === 'cmd1'" style="color: #28a745; font-size: 0.9em; margin-top: -0.25rem; margin-bottom: 0.5rem;">复制成功!</div>
          <p style="font-size: 0.8rem; color: #718096; margin-top: 0.75rem;">请复制上方脚本到您的服务器终端执行</p>
        </div>

        <div class="method-card">
          <div style="display: flex; align-items: center; margin-bottom: 0.75rem;">
            <h3 style="font-size: 1.125rem; font-weight: 600; margin-top: 0;">方法 2: 使用Docker安装</h3>
          </div>
          <p style="font-size: 0.9rem; color: #4a5568; margin-bottom: 0.1rem;">首先，您需要在您的服务器上安装 Docker。</p>
          <div style="display: flex; align-items: center; gap: 0.5rem; margin-bottom: 0.5rem;">
            <pre><code>{{ command2aText }}</code></pre>
            <button @click="triggerCopy(command2aText, 'cmd2a')" :style="copyIconButtonBaseStyle" title="复制命令" class="copy-button">
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" :style="copyIconSvgStyle"><path d="M16 1H4c-1.1 0-2 .9-2 2v14h2V3h12V1zm3 4H8c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h11c1.1 0 2-.9 2-2V7c0-1.1-.9-2-2-2zm0 16H8V7h11v14z"/></svg>
            </button>
          </div>
          <div v-if="isSuccess && lastCopiedId === 'cmd2a'" style="color: #28a745; font-size: 0.9em; margin-top: -0.25rem; margin-bottom: 0.5rem;">复制成功!</div>
          
          <p style="font-size: 0.9rem; color: #4a5568; margin-top: 1.5rem; margin-bottom: 0.1rem;">然后复制下面命令到您的服务器终端执行</p>
          <div style="display: flex; align-items: center; gap: 0.5rem; margin-bottom: 0.5rem;">
            <pre><code>{{ command2bText }}</code></pre>
            <button @click="triggerCopy(command2bText, 'cmd2b')" :style="copyIconButtonBaseStyle" title="复制命令" class="copy-button">
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" :style="copyIconSvgStyle"><path d="M16 1H4c-1.1 0-2 .9-2 2v14h2V3h12V1zm3 4H8c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h11c1.1 0 2-.9 2-2V7c0-1.1-.9-2-2-2zm0 16H8V7h11v14z"/></svg>
            </button>
          </div>
          <div v-if="isSuccess && lastCopiedId === 'cmd2b'" style="color: #28a745; font-size: 0.9em; margin-top: -0.25rem; margin-bottom: 0.5rem;">复制成功!</div>
        </div>

        <div class="method-card">
          <div style="display: flex; align-items: center; margin-bottom: 0.75rem;">
            <h3 style="font-size: 1.125rem; font-weight: 600; margin-top: 0;">方法 3: 通过宝塔面板的Docker一键安装</h3>
          </div>
          <p style="font-size: 1.0rem; color: #4a5568; margin-bottom: 0.1rem;">安装好宝塔面板 > 侧边栏【Docker】> Docker应用商店搜【ALLinSSL】一键安装</p>

        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import { useClipboard } from '../composables/useClipboard.js';

const command1Text = 'curl -sSO http://download.allinssl.com/install_allinssl.sh && bash install_allinssl.sh allinssl';
const command2aText = 'bash <(wget -qO- https://get.docker.com)';
const command2bText = 'docker run -itd --name allinssl -p 7979:8888 -v /www/allinssl/data:/www/allinssl/data -e ALLINSSL_USER=allinssl -e ALLINSSL_PWD=allinssldocker -e ALLINSSL_URL=allinssl allinssl/allinssl:latest';

const { isSuccess, copyToClipboard } = useClipboard();
const lastCopiedId = ref(null);

const triggerCopy = (textToCopy, commandId) => {
  copyToClipboard(textToCopy);
  lastCopiedId.value = commandId;
};

// Base style for the icon button
const copyIconButtonBaseStyle = {
  padding: '10px', // Increased padding
  backgroundColor: 'transparent',
  border: 'none',
  borderRadius: '4px',
  cursor: 'pointer',
  display: 'flex',
  alignItems: 'center',
  justifyContent: 'center',
  flexShrink: 0, // Prevent button from shrinking
};

// Style for the SVG icon itself
const copyIconSvgStyle = computed(() => ({
  width: '18px', // Icon size
  height: '18px',
  // fill: '#666', // Color handled by CSS now
  transition: 'fill 0.2s ease',
}));

</script>

<style scoped>
.copy-button svg {
  fill: #666; /* Default icon color for light mode */
}
.copy-button svg:hover {
  fill: #333; /* Darker color on hover for light mode */
}

.self-hosted-setup-section {
  margin-top: 4rem;
  margin-bottom: 4rem;
  padding: 2rem; /* Default padding */
}

.columns-container {
  display: flex; /* Defaults to flex-wrap: nowrap; which forces side-by-side */
  align-items: flex-start; /* Align items to the top */
  gap: 2rem; /* Default gap between image and text column */
}

.image-column {
  flex: 0 0 382px; /* Do not grow, do not shrink, basis is 280px */
}

.text-content-column {
  flex: 1 1 auto; /* Grow to fill available space, shrink if needed, basis is auto */
  min-width: 0; /* Allows the column to shrink below its content intrinsic size */
  display: flex;
  flex-direction: column;
  gap: 1.5rem; /* Default gap between method blocks */
}

.method-card {
  background-color: white;
}

/* Modern scrollbar for <pre> elements - default to subtle/hidden */
pre {
  background-color: #f7fafc;
  padding: 0.75rem;
  border-radius: 0.25rem;
  overflow-x: auto;
  flex-grow: 1;
  /* Existing scrollbar styles */
  scrollbar-width: thin;
  scrollbar-color: transparent transparent;
  /* Transition for scrollbar visibility (works for some properties in some browsers) */
  transition: scrollbar-color 0.3s ease-out;
}

pre:hover {
  scrollbar-color: #c1c1c1 #f1f1f1; /* For Firefox - thumb and track color on hover */
}

pre::-webkit-scrollbar {
  width: 8px;
  height: 8px;
  background-color: transparent; /* Make scrollbar background transparent by default */
}

pre::-webkit-scrollbar-track {
  background: transparent; /* Transparent track by default */
  border-radius: 10px;
}

pre::-webkit-scrollbar-thumb {
  background: transparent; /* Transparent thumb by default */
  border-radius: 10px;
  /* Add a transition for smoother appearance */
  transition: background 0.2s ease-in-out;
}

/* Show scrollbar thumb and track on hover of the <pre> element */
pre:hover::-webkit-scrollbar-track {
  background: #f1f1f1;
}

pre:hover::-webkit-scrollbar-thumb {
  background: #c1c1c1;
}

/* Darker thumb when scrollbar thumb itself is hovered (and <pre> is also hovered) */
pre:hover::-webkit-scrollbar-thumb:hover {
  background: #a1a1a1;
}

/* Mobile Optimizations */
@media (max-width: 768px) {
  .self-hosted-setup-section {
    padding: 1rem; /* Reduced padding for mobile */
    margin-top: 2rem;
    margin-bottom: 2rem;
  }

  .columns-container {
    gap: 1.5rem; /* Reduced gap for mobile, items will stack due to rules below */
    /* No need to change flex-direction if image-column is display:none 
       and text-content-column takes full width */
  }

  .image-column {
    display: none; /* Hide the image column on mobile */
  }

  .text-content-column {
    flex: 0 0 100%; /* Do not grow/shrink, basis is 100% (full width) */
    /* min-width: 0; is still good practice */
    gap: 1rem; /* Reduced gap between method blocks on mobile */
    /* Other mobile-specific font/padding adjustments below */
  }

  h3 {
    font-size: 1rem; /* Slightly smaller h3 on mobile */
  }
  p, pre /* Apply to pre as well for code block text */ {
    font-size: 0.85rem; /* Adjust base text and code size for readability */
  }
   .copy-button svg {
     width: 20px;
     height: 20px;
  }
}

@media (max-width: 480px) {
    .self-hosted-setup-section {
        padding: 0.75rem;
    }
     h3 {
        font-size: 0.95rem;
    }
    p, pre {
        font-size: 0.8rem; 
    }
}

/* Dark Mode Adaptations */
html.dark .self-hosted-setup-section {
  /* background-color: #1e1e1e; */ /* Example dark background for the whole section */
}

html.dark .method-card {
  background-color: #25252A;
  border-color: #3a3a3a;
}

/* Text colors in dark mode */
html.dark h3 {
  color: #e0e0e0; /* Lighter text for headings */
}

html.dark p,
html.dark .method-card p[style*="color: #4a5568"],
html.dark .method-card p[style*="color: #718096"] {
  color: #adbac7; /* Lighter text for paragraphs and helper texts */
}

html.dark div[style*="color: #28a745"] { /* "复制成功!" message */
  color: #34d399; /* Adjust green for better visibility on dark, or keep as is if contrast is good */
}

/* Code blocks in dark mode */
html.dark pre {
  background-color: #1e1e2e; /* No !important needed now */
}
html.dark pre code {
   color: #c9d1d9; /* Example: light text for code */
}


/* Copy icon in dark mode */
html.dark .copy-button svg {
  fill: #999; /* Lighter icon color for dark mode */
}
html.dark .copy-button svg:hover {
  fill: #ccc; /* Even lighter on hover in dark mode */
}

/* Scrollbars in dark mode */
html.dark pre {
  scrollbar-color: #555 #333; /* For Firefox - thumb and track color */
}

html.dark pre:hover {
  scrollbar-color: #6b6b6b #3a3a3a; /* For Firefox - thumb and track color on hover */
}

html.dark pre::-webkit-scrollbar-track {
  background: transparent; /* Keep track transparent or a very dark grey */
}
html.dark pre:hover::-webkit-scrollbar-track {
  background: #2c2c2d; /* Dark track on hover */
}

html.dark pre::-webkit-scrollbar-thumb {
  background: transparent; /* Keep thumb transparent or a very dark grey */
}
html.dark pre:hover::-webkit-scrollbar-thumb {
  background: #5a5a5f; /* Dark thumb on hover */
}

html.dark pre:hover::-webkit-scrollbar-thumb:hover {
  background: #7a7a7f; /* Slightly lighter dark thumb when directly hovered */
}

/* Ensure mobile styles also respect dark mode if specific colors were set */
@media (max-width: 768px) {
  html.dark h3 {
    /* color: #e0e0e0; Already covered */
  }
  html.dark p, html.dark pre {
    /* color: #adbac7; Already covered */
  }
}
</style> 