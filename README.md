# 🐸 ShrekScript - WhatsApp Web Spammer

Um script para enviar o roteiro completo do filme Shrek (ou qualquer texto) linha por linha no WhatsApp Web.

![Shrek](https://media.giphy.com/media/DpB9NBjny7jF1pd0yt2/giphy.gif)

## ⚠️ Aviso

Este projeto é apenas para **fins educacionais e de entretenimento**. Use com responsabilidade e apenas com pessoas que consentiram receber centenas de mensagens.

## 🚀 Como usar

### 1. Abra o WhatsApp Web
Acesse [web.whatsapp.com](https://web.whatsapp.com) e faça login.

### 2. Abra uma conversa
Selecione o contato que vai receber o script (de preferência alguém com bom humor).

### 3. Abra o Console do navegador
- **Chrome/Edge:** `F12` → aba `Console`
- **Firefox:** `F12` → aba `Console`
- **Mac:** `Cmd + Option + J`

### 4. Cole o script
```javascript
async function enviarScript(scriptText){
    const lines = scriptText.split(/[\n\t]+/).map(line => line.trim()).filter(line => line);
    main = document.querySelector("#main"),
    textarea = main.querySelector(`div[contenteditable="true"]`)
    
    if(!textarea) throw new Error("Não há uma conversa aberta")
    
    for(const line of lines){
        console.log(line)
    
        textarea.focus();
        document.execCommand('insertText', false, line);
        textarea.dispatchEvent(new Event('change', {bubbles: true}));
    
        setTimeout(() => {
            (main.querySelector(`[aria-label="Enviar"]`) || main.querySelector(`[data-icon="send"]`)).click();
        }, 100);
        
        if(lines.indexOf(line) !== lines.length - 1) await new Promise(resolve => setTimeout(resolve, 250));
    }
    
    return lines.length;
}

enviarScript(`
COLE SEU TEXTO AQUI
`).then(e => console.log(`✅ Finalizado! ${e} mensagens enviadas`)).catch(console.error)
```

### 5. Pressione Enter e aguarde
O script vai enviar cada linha como uma mensagem separada.

## ⚙️ Configurações

### Alterar o delay entre mensagens
Modifique o valor `250` (em milissegundos) na linha:
```javascript
await new Promise(resolve => setTimeout(resolve, 250));
```

- `250` = 0.25 segundos (rápido)
- `1000` = 1 segundo (moderado)
- `2000` = 2 segundos (seguro)

### Seletor do botão de enviar
Se o script não funcionar, o WhatsApp pode ter atualizado os seletores. Tente trocar:
```javascript
main.querySelector(`[aria-label="Enviar"]`)
```
Por uma dessas alternativas:
```javascript
main.querySelector(`[data-testid="send"]`)
main.querySelector(`[data-icon="send"]`)
main.querySelector(`button span[data-icon="send"]`).parentElement
```

## 🛠️ Troubleshooting

| Problema | Solução |
|----------|---------|
| "Não há uma conversa aberta" | Abra uma conversa antes de executar |
| Mensagem digita mas não envia | Troque o seletor do botão de enviar |
| Script para no meio | WhatsApp pode ter limitado, aguarde e tente novamente |
| `null is not an object` | Seletor desatualizado, inspecione o botão e atualize |

## 📝 Exemplos de uso

### Texto customizado
```javascript
enviarScript(`
Linha 1
Linha 2
Linha 3
`)
```

### Spam simples
```javascript
enviarScript(`${'🐸\n'.repeat(100)}`)
```

## 📜 Licença

```
            DO WHAT THE FUCK YOU WANT TO PUBLIC LICENSE
                    Version 2, December 2004

 Copyright (C) 2004 Sam Hocevar <sam@hocevar.net>

 Everyone is permitted to copy and distribute verbatim or modified
 copies of this license document, and changing it is allowed as long
 as the name is changed.

            DO WHAT THE FUCK YOU WANT TO PUBLIC LICENSE
   TERMS AND CONDITIONS FOR COPYING, DISTRIBUTION AND MODIFICATION

  0. You just DO WHAT THE FUCK YOU WANT TO.
```

---

**Lembre-se:** Com grandes poderes vêm grandes responsabilidades. Use com sabedoria. 🧅

*"Ogros são como cebolas. Cebolas têm camadas. Ogros têm camadas."* - Shrek
