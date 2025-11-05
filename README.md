# AnimeFire Downloader

Uma extensão Chrome poderosa e inteligente para download de episódios de anime do site **AnimeFire.plus**. Com suporte a múltiplas qualidades, downloads em lote, controle de fila e técnicas avançadas de anti-detecção.

[![Chrome Web Store](https://img.shields.io/badge/Chrome%20Extension-Manifest%20V3-green.svg)](https://github.com/e43b/AnimeFire-Downloader)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![GitHub Stars](https://img.shields.io/github/stars/e43b/AnimeFire-Downloader.svg)](https://github.com/e43b/AnimeFire-Downloader)

## Recursos Principais

### 📥 Download Inteligente
- **Download automático** de episódios individuais
- **Download em massa** de múltiplos episódios
- **Download em lote** com lista de links
- **Detecção automática** de episódios na página
- Organização automática em pastas por anime

### 🎬 Suporte Múltiplas Qualidades
- FullHD (melhor qualidade)
- F-HD (Full HD alternativo)
- HD (Alta definição)
- SD (Definição padrão)
- Seleção automática da melhor qualidade disponível

### ⚡ Controle de Fila Avançado
- **Limite de downloads simultâneos** (configurável entre 1-5)
- **Fila inteligente** que gerencia requisições automaticamente
- **Priorização** de downloads
- **Pausa/Retomada** de downloads
- Visualização de progresso em tempo real

### 🛡️ Anti-Detecção
- **Rotação de User-Agents** (6 navegadores diferentes)
- **Delays dinâmicos** entre requisições (2-8 segundos base)
- **Backoff exponencial** para rate limiting
- **Múltiplas estratégias de fallback** (proxy headers, minimal headers)
- **Headers realistas** (Accept, Referer, DNT, etc.)
- Detecção e adaptação automática a bloqueios 429/403

### ⚙️ Configurações Personalizáveis
- Intervalo entre downloads (1-60 segundos)
- Quantidade máxima de downloads simultâneos (1-5)
- Opção de baixar todas as qualidades
- Detecção automática de episódios
- Notificações de progresso
- Organização de pastas customizável

### 🎯 Interface Amigável
- **Popup elegante** com 3 abas principais
- **Integração visual** no site do AnimeFire
- **Botões de download** injetados em episódios
- **Modal de progresso** com status de cada download
- **Notificações em tempo real** (sucesso, erro, info)

## Instalação

### Via GitHub (Desenvolvimento)

1. Clone o repositório:
```bash
git clone https://github.com/e43b/AnimeFire-Downloader.git
cd AnimeFire-Downloader
```

2. Abra Chrome e acesse `chrome://extensions/`

3. Ative **"Modo de desenvolvedor"** (canto superior direito)

4. Clique em **"Carregar extensão sem empacotamento"**

5. Selecione a pasta do projeto

6. A extensão agora está instalada e ativa!

## Como Usar

### Download de Episódio Único
1. Navegue para uma página de episódio em **animefire.plus**
2. Clique no ícone da extensão
3. Escolha a qualidade desejada
4. Clique em **"Baixar Episódio"**

### Download de Todos os Episódios
1. Acesse a página principal de um anime
2. Clique no ícone da extensão
3. Insira o intervalo (ex: episódios 1 a 25)
4. Escolha a qualidade
5. Clique em **"Baixar Episódios"**

### Download em Lote
1. Clique na aba **"Download em Lote"**
2. Cole os links dos episódios (um por linha):
```
https://animefire.plus/animes/one-piece/1
https://animefire.plus/animes/one-piece/2
https://animefire.plus/animes/one-piece/3
```
3. Escolha a qualidade
4. Clique em **"Baixar Todos"**

### Integração com o Site
- Botões de download aparecem automaticamente nos episódios
- Clique no ícone de download nos episódios individuais
- Menu de contexto (clique direito) com opções de download

## Configurações

### Intervalo entre Downloads
Define o tempo de espera entre requisições sucessivas (1-60s). Valores maiores são mais seguros contra bloqueios.

**Padrão:** 20 segundos

### Downloads Simultâneos Máximos
Controla quantos downloads podem rodar ao mesmo tempo (1-5).

**Padrão:** 2 downloads simultâneos

### Baixar Todas as Qualidades
Quando ativado, faz download de todas as qualidades disponíveis do episódio.

**Padrão:** Desativado

### Detectar Automaticamente
Analisa a página atual e detecta automaticamente se é episódio ou anime.

**Padrão:** Ativado

### Mostrar Notificações
Exibe notificações no navegador com status dos downloads.

**Padrão:** Ativado

## Arquitetura

```
AnimeFire-Downloader/
├── manifest.json           # Configuração da extensão
├── background.js           # Service Worker (processamento em background)
├── content.js              # Script injatado nas páginas
├── content.css             # Estilos dos botões injetados
├── popup.html              # Interface da extensão
├── popup.js                # Lógica da interface
├── popup.css               # Estilos da interface
├── README.md               # Este arquivo
└── LICENSE                 # Licença do projeto
```

## Componentes Técnicos

### Background Service Worker (`background.js`)
- Gerencia downloads via Chrome Downloads API
- Implementa sistema de fila e limites simultâneos
- Realiza requisições stealth com anti-detecção
- Extrai links de qualidade das páginas
- Menu de contexto

### Content Script (`content.js`)
- Injeta botões de download no site
- Detecta mudanças dinâmicas de página
- Comunica com background via message passing
- Extrai informações de episódios e animes

### Popup Interface (`popup.js`)
- Gerencia configurações do usuário
- Detecta página atual (episódio/anime)
- Controla fila de downloads
- Exibe progresso em tempo real
- Interface com 3 abas (Atual, Lote, Configurações)

## Melhorias Implementadas

### Sistema de Fila Inteligente
- Mantém lista de downloads pendentes
- Respeita limite de simultâneos (configurável)
- Inicia próximos downloads automaticamente
- Priorização baseada na ordem

### Anti-Detecção Avançada
- User-Agent rotation entre 6 navegadores
- Delays dinâmicos que aumentam com requisições
- Backoff exponencial para rate limiting
- Fallbacks automáticos para estratégias alternativas
- Tratamento de erros 429 (rate limit) e 403 (blocked)

### Performance
- Debounce em observers de mutação
- Delays aleatórios para evitar padrões
- Cache de links de qualidade
- Requisições otimizadas com headers realistas

### Experiência do Usuário
- Detecção automática de contexto
- Notificações em tempo real
- Modal de progresso com status individual
- Interface responsiva e intuitiva
- Persistência de configurações

## Troubleshooting

### Downloads não funcionam
1. Verifique se está em animefire.plus
2. Tente aumentar o intervalo entre downloads nas configurações
3. Limpe o cache da extensão (remova e reinstale)

### Recebe mensagem "Qualidade não disponível"
- O site pode estar indisponível temporariamente
- Tente novamente em alguns minutos
- Tente com outra qualidade

### Extensão não aparece
1. Vá em `chrome://extensions/`
2. Ative o "Modo de desenvolvedor"
3. Clique em "Carregar extensão sem empacotamento"
4. Selecione a pasta do projeto

### Downloads lentos
- Aumente o intervalo entre downloads nas configurações
- Reduz o número máximo de downloads simultâneos
- Verifique sua conexão de internet

## Limitações Conhecidas

- Funciona apenas em Chrome/Chromium (Manifest V3)
- Depende da disponibilidade do site AnimeFire.plus
- Qualidades disponíveis variam por episódio
- Downloads respeitam as limitações do servidor

## Considerações Legais

Esta extensão é fornecida apenas para fins educacionais. Os usuários são responsáveis por respeitar os direitos autorais e os termos de serviço do AnimeFire.plus.

## Contribuições

Contribuições são bem-vindas! Sinta-se à vontade para:
- Reportar bugs (abra uma issue)
- Sugerir melhorias
- Enviar pull requests com novos recursos
- Melhorar a documentação

## Roadmap

- [ ] Suporte para múltiplos sites de anime
- [ ] Pausa/Retomada de downloads
- [ ] Histórico de downloads
- [ ] Temas personalizáveis (dark mode)
- [ ] Integração com API de dados de animes

## Autor

Desenvolvido e mantido por **[E43b](https://github.com/e43b)**

## Links Úteis

- **GitHub:** https://github.com/e43b/AnimeFire-Downloader
- **AnimeFire:** https://animefire.plus/
- **Issues:** https://github.com/e43b/AnimeFire-Downloader/issues
- **Discord:** https://discord.gg/GgBbbjDkXu

## Licença

Este projeto está licenciado sob a Licença MIT - veja o arquivo [LICENSE](LICENSE) para detalhes.

---

**Nota:** Esta extensão é um projeto de código aberto e não é afiliada ao AnimeFire.plus. Use responsavelmente e respeite os direitos autorais.
