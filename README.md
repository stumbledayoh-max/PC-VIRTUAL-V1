<h1 align="center">☁️ CROWCLOUD</h1>
<h3 align="center"><i>Play beyond the sky</i></h3>

<p align="center">
Um Windows completo rodando na nuvem do GitHub, acessível pelo <b>navegador</b> ou por <b>RDP</b>.<br>
Instala sozinho, vem com o wallpaper CrowCloud, ativa com a sua key e <b>salva seus apps e arquivos</b>.
</p>

---

# 📋 O QUE VOCÊ PRECISA

# ✅ 1. Uma conta no GitHub
# ✅ 2. Uma conta grátis no Tailscale
# ✅ 3. (Opcional) Uma key do Windows para ativar

> 💡 **Use um repositório PÚBLICO.** Nele o GitHub dá **4 CPUs e 16 GB de RAM** e libera o KVM, que o Windows precisa para rodar rápido. Em repositório privado a máquina é bem menor (2 CPUs, 7 GB) e o KVM pode não existir.

---

# 🚀 PASSO A PASSO

---

# 🔑 PASSO 1: Criar a conta do Tailscale

O Tailscale é a "ponte" segura entre o seu aparelho e o Windows na nuvem.

1. Crie a conta grátis em **tailscale.com** (pode entrar com Google).
2. Instale o app do **Tailscale** no aparelho que vai usar (celular ou PC) e entre com essa conta.

> ✅ **Não precisa criar chave nem secret.** O login é feito por um **link**, a cada vez que você ligar o Windows (veja o passo 6).

---

# 🔒 PASSO 2: (Opcional) Guardar a key do Windows

Só se você quiser que o Windows seja **ativado sozinho**.

No repositório, vá em:

**Settings → Secrets and variables → Actions → New repository secret**

| Nome | Valor |
|---|---|
| `WINDOWS_KEY` | sua key (`XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`) |

> 🔐 O secret nunca aparece nos logs. Se não tiver key, **pule este passo**.

---

# 📁 PASSO 3: Colocar o arquivo no repositório

É **UM arquivo só**. Crie este caminho exatamente assim:

```
.github/workflows/windows-docker.yml
```

Cole dentro dele o conteúdo do arquivo `windows-docker.yml`.

> 🖼️ O wallpaper e todos os scripts **já estão dentro desse arquivo**. Não precisa subir mais nada.

---

# ⚙️ PASSO 4: Liberar a permissão

Vá em:

**Settings → Actions → General → Workflow permissions**

Marque **Read and write permissions** e clique em **Save**.

> Sem isso o workflow não consegue salvar o seu disco do Windows.

---

# ▶️ PASSO 5: Iniciar o Windows

1. Abra a aba **Actions** do repositório.
2. Clique em **Windows Docker** (menu da esquerda).
3. Clique em **Run workflow**.
4. Escolha as opções (veja a tabela abaixo) ou **deixe tudo como está**.
5. Clique no botão verde **Run workflow**.

### 🎛️ As opções

| Opção | O que faz | Padrão |
|---|---|---|
| **Sistema** | Qual Windows instalar (lista completa abaixo) | Windows 10 Pro |
| **Usuário** | Nome do usuário do Windows | vazio = `CrowCloud` |
| **Senha** | Senha do Windows | vazio = `CrowCloud` |
| **RAM** | Memória da máquina virtual | `13G` |
| **CPUs** | Núcleos da máquina virtual | `4` |
| **Disco** | Tamanho do disco virtual | `80G` |
| **Salvar apps e dados** | Guarda o disco inteiro para a próxima vez | ✅ ligado |
| **Reiniciar sozinho** | Modo servidor: começa outra execução ao fim das ~5h | ❌ desligado |

> 💡 Em repositório **privado**, troque a RAM para `4G` e as CPUs para `2`.

---

# 💻 SISTEMAS DISPONÍVEIS

### 🪟 Windows 11
- **11**: Pro (completo, sem ativação)
- **11l**: LTSC (enxuto, suporte longo, avaliação)
- **11e**: Enterprise (corporativo, avaliação)

### 🪟 Windows 10
- **10**: Pro (**padrão**)
- **10l**: LTSC (enxuto, suporte longo, avaliação)
- **10e**: Enterprise (corporativo, avaliação)

### 🖥️ Windows Server (avaliação de 180 dias)
- **2025**, **2022**, **2019**, **2016**, **2012**, **2008**, **2003**

### 🕰️ Windows antigos
- **8e**: Windows 8.1 Enterprise
- **7u**: Windows 7 Ultimate
- **vu**: Windows Vista Ultimate
- **xp**: Windows XP Professional
- **2k**: Windows 2000 Professional (sem RDP)

> ⚠️ Nos sistemas **antigos** (8.1, 7, Vista, XP, 2000, Server 2003 e 2008) o wallpaper e a ativação automática podem não funcionar.

---

# 🔗 PASSO 6: Entrar pelo link do Tailscale

Quando você inicia o Windows, o GitHub gera um **link de login**. Você precisa abri-lo **uma vez a cada execução**.

1. Clique na execução que acabou de começar (aba **Actions**).
2. Na página da execução, role até **Summary**. Vai aparecer o título **🔗 Login do Tailscale** com o link grande.
   (Se não aparecer, abra a etapa **Tailscale - gerar link de login** e copie o link do log.)
3. Abra o link, entre na **sua conta do Tailscale** e clique em **Connect**.

> ⏱️ Você tem cerca de **20 minutos** para abrir o link. Depois disso a execução falha: é só rodar de novo.

---

# 📱 PASSO 7: Entrar no Windows

### 1️⃣ Deixe o Tailscale ligado no aparelho que vai usar
- Abra o app do **Tailscale** (instalado no passo 1).
- Confira que está na **mesma conta** do link do passo 6.
- Deixe a **VPN ligada**.

### 2️⃣ Pegue o endereço
Abra a execução na aba **Actions**, entre na etapa **Show access info**. Vai aparecer um quadro assim:

```
NAVEGADOR: http://100.x.x.x:8006
RDP:       100.x.x.x:3389
Usuário:   CrowCloud
Senha:     CrowCloud
```

### 3️⃣ Escolha como acessar

| Jeito | Como |
|---|---|
| 🌐 **Navegador** (mais fácil) | Abra `http://100.x.x.x:8006` |
| 🖥️ **RDP** (melhor qualidade) | Use o app *Conexão de Área de Trabalho Remota* (Windows) ou *Microsoft Remote Desktop* (celular) |

> ⚠️ Digite **`http://`** e não `https://`. O endereço só funciona com `http`.

---

# ⏳ NA PRIMEIRA VEZ

A **primeira execução** baixa e instala o Windows sozinho. Isso leva de **20 a 40 minutos**.

Você pode **acompanhar pelo navegador** (porta 8006) enquanto instala.

Quando o log mostrar **`Windows PRONTO ✓`**, já pode usar.

> 🔁 Da **segunda vez em diante**, o seu disco é restaurado e o Windows **sobe em poucos minutos**, com tudo no lugar.

---

# 💾 COMO SALVA SEUS APPS E DADOS

Ao encerrar, o workflow:

1. Desliga o Windows com calma.
2. Comprime o disco inteiro.
3. Envia para uma **Release privada** do seu repositório.

Na próxima execução, ele **baixa e restaura** esse disco. Por isso os **programas instalados e os arquivos voltam**.

> 📦 Cada sistema tem o **seu próprio backup**. O backup antigo só é apagado depois que o novo foi enviado com sucesso.

---

# 🛑 COMO ENCERRAR SEM PERDER NADA

# ✅ Desligue o Windows pelo menu Iniciar

O workflow percebe, **salva tudo com calma** e termina sozinho.

# ❌ Evite o botão "Cancel workflow"

O GitHub dá pouco tempo para salvar depois de um cancelamento, e o backup pode ficar **incompleto**.

> ⏰ Se você não fizer nada, o workflow se encerra e salva sozinho depois de **5h15**.

---

# 🔑 ATIVAÇÃO AUTOMÁTICA

Se você criou o secret **`WINDOWS_KEY`**, o Windows é ativado sozinho.

- Funciona **a cada inicialização**, inclusive nos discos restaurados.
- No **Server de avaliação**, ele converte a edição, reinicia e ativa.
- O resultado fica em `C:\OEM\activate.log` dentro do Windows.
- A key **nunca aparece nos logs**.

> ⚠️ A key precisa ser da **mesma edição** instalada (Pro com Pro, Server Standard com Server Standard).

---

# 🔁 MODO SERVIDOR

Ligue a opção **Reiniciar sozinho** para o Windows ficar quase sempre no ar.

Ao fim das ~5h, o workflow **começa outra execução** e restaura o seu disco.

Se você **desligar o Windows** pelo menu Iniciar, ele **não** reinicia.

> ⚠️ Deixar a máquina ligada quase o tempo todo pode ir contra os termos de uso do GitHub Actions. Use por sua conta e risco.

---

# 🔧 PROBLEMAS COMUNS

| Problema | Solução |
|---|---|
| **"Este runner não tem /dev/kvm"** | Use um repositório **público** |
| **Erro ao criar a Release** | Faça o **passo 4** (permissão *Read and write*) |
| **"A conexão expirou" no navegador** | Confira se o Tailscale está **ligado** no aparelho e se o endereço começa com **`http://`** |
| **"Login do Tailscale não foi feito a tempo"** | Rode o workflow de novo e abra o link do **passo 6** em até 20 min |
| **Não achei o link de login** | Abra a etapa **Tailscale - gerar link de login** no log e copie o endereço que aparece |
| **Aparecem aparelhos `gh-...` antigos no Tailscale** | Normal: apague os antigos em *login.tailscale.com/admin/machines* |
| **Senha não funciona depois de restaurar** | Valem o **usuário e a senha da primeira instalação**, não os do formulário |
| **Windows não ativa** | Veja o `C:\OEM\activate.log` e confira se a key é da **edição certa** |
| **Cores ruins no celular** | No app/navegador, coloque a qualidade da imagem no **máximo** |

---

# ⚠️ AVISOS IMPORTANTES

- 🔐 A senha padrão (`CrowCloud`) é **fraca**. Use **apenas pelo Tailscale**, nunca abra as portas para a internet.
- 📜 O Windows é baixado da Microsoft **sem ativação**. A **licença é por sua conta**.
- 🧪 Os **Servers, LTSC e Enterprise** vêm como versão de **avaliação**.
- 💽 O limite de espaço é de cerca de **65 GB**. Arquivos muito grandes é melhor guardar fora.
- ⚖️ Rodar um desktop remoto em runners do GitHub pode ir contra os **termos de uso do GitHub Actions**. Use por sua conta e risco.

---

<h3 align="center">☁️ CrowCloud — <i>Play beyond the sky</i></h3>
