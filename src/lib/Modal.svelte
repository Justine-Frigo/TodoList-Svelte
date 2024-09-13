<script>
    export let showModal = false;
    export let closeModal;
  
    const handleOverlayClick = (e) => {
      if (e.target.classList.contains('modal-overlay')) {
        closeModal();
      }
    };
  </script>
  
  {#if showModal}
    <div class="modal-overlay" on:click={handleOverlayClick}>
      <div class="modal">
        <slot></slot>
        <button class="close-btn" on:click={closeModal}>Close</button>
      </div>
    </div>
  {/if}
  
  <style>
    .modal-overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.5);
      display: flex;
      justify-content: center;
      align-items: center;
    }
  
    .modal {
      background: white;
      padding: 20px;
      border-radius: 10px;
      width: 300px;
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
    }
  
    .close-btn {
      background: #ff6f00;
      border: none;
      color: white;
      padding: 10px;
      cursor: pointer;
      margin-top: 10px;
    }
  </style>
  