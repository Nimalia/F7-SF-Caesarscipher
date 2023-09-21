new Vue({
    el: '#app',
    data: {
      message: '',
      shift: 0,
      cipher: '',
    },
    methods: {
      encrypt() {
        const alphabet = 'АБВГДЕЁЖЗИЙКЛМНОПРСТУФХЦЧШЩЬЫЭЮЯ';
        let result = '';

        for (let i = 0; i < this.message.length; i++) {
          let char = this.message[i];
          if (char === ' ') {
            result += ' ';
          } else {
            let charIndex = alphabet.indexOf(char.toUpperCase());
            if (charIndex !== -1) {
              let shiftedIndex = (charIndex + this.shift) % alphabet.length;
              if (shiftedIndex < 0) {
                shiftedIndex += alphabet.length;
              }
              let shiftedChar = alphabet[shiftedIndex];
              result += char === char.toUpperCase() ? shiftedChar : shiftedChar.toLowerCase();
            } else {
              result += char;
            }
          }
        }
        this.cipher = result;
      },
      decrypt() {
        this.shift = -this.shift;
        this.encrypt();
        this.shift = -this.shift;
      },
    },
  });