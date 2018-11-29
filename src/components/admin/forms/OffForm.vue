<template>
  <div class="modal">
    <div class="modal-content">
      <form>
        <label class="title">Desconto por categoria</label>
        <label>Categoria</label>
        <select class="select-field">
          <option value="medicamento" selected>Medicamentos</option>
          <option value="higiene">Higiene pessoal</option>
          <option value="cosmetico">Cosméticos</option>
          <option value="alimento">Alimentos</option>
        </select>
        <label>Desconto</label>
        <label class="radio-container">Sem desconto (0%)
          <input type="radio" name="desconto" value="0"><span class="checkmark"></span>
        </label>
        <label class="radio-container">Bom desconto (10%)
          <input type="radio" name="desconto" value="10"><span class="checkmark"></span>
        </label>
        <label class="radio-container">Ótimo desconto (25%)
          <input type="radio" name="desconto" value="25"><span class="checkmark"></span>
        </label>
        <label class="radio-container">Super desconto (50%)
          <input type="radio" name="desconto" value="50"><span class="checkmark"></span>
        </label>
        <div class="btn-group">
          <button @click="$emit('close')" class="btn-cancel">Cancelar</button>
          <button @click="registerOffSale()" class="btn-confirm">Aplicar desconto</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'OffForm',
  methods: {
    registerOffSale () {
      alert('Cadastrado com sucesso')
      this.closeForm()
    }
  }
}
</script>

<style lang="scss" scoped>
  @import 'src/assets/css/forms.scss';
</style>
