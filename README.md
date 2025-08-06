# 🛡️ WordPress Secure Blueprint

Blueprint completo para criação de um site WordPress seguro e bem estruturado, com ambiente de desenvolvimento via **LocalWP**, preparação de arquivos e checklist de segurança baseado na **ISO/IEC 27001**.

---

## 🚀 1. Instalação com LocalWP

### Pré-requisitos
- [LocalWP](https://localwp.com/) instalado
- PHP ≥ 8.0, MySQL ≥ 5.7
- Acesso à internet para baixar WordPress

### Passo a passo

1. **Criar novo site**
   - Abra o LocalWP
   - Clique em "Create a New Site"
   - Nomeie seu site (`meusite-seguro`)
   - Selecione ambiente **Custom**: PHP 8+, Nginx ou Apache, MySQL 5.7+
   - Crie o site

2. **Configurar wp-config.php**
   - Gere as chaves de segurança:  
     https://api.wordpress.org/secret-key/1.1/salt/
   - Defina no `wp-config.php`:
     ```php
     define('DISALLOW_FILE_EDIT', true);
     define('FORCE_SSL_ADMIN', true);
     ```

3. **Instale tema/plugin do projeto**
   - Copie seus arquivos personalizados para:
     ```
     app/public/wp-content/themes/
     app/public/wp-content/plugins/
     ```

4. **Ajuste permissões de arquivos** (Linux/macOS)
   ```bash
   find . -type f -exec chmod 644 {} \;
   find . -type d -exec chmod 755 {} \;
   chmod 600 wp-config.php

## ✅  2. Checklist de Segurança para WordPress

### 🔐 1. Infraestrutura
- [ ] Servidor com PHP, MySQL/MariaDB e Apache/Nginx atualizados
- [ ] Exibição de erros desabilitada em produção
- [ ] Listagem de diretórios desabilitada
- [ ] Permissões seguras em arquivos e pastas (`644` para arquivos, `755` para pastas, `600` para `wp-config.php`)
- [ ] HTTPS habilitado com redirecionamento automático
- [ ] Firewall de aplicação (WAF) ativo (ex: Cloudflare, Imunify360)
- [ ] XML-RPC desabilitado, se não utilizado

## 🔑 2. Acesso e Autenticação
- [ ] Usuário admin com nome personalizado (evitar `admin`)
- [ ] Senhas fortes e únicas para todos os usuários
- [ ] Autenticação em duas etapas (2FA) habilitada
- [ ] Desabilitar login por e-mail (se possível)
- [ ] Limitar tentativas de login (plugin recomendado)
- [ ] Registro de logins e falhas de login

## 🧱 3. Arquitetura WordPress
- [ ] Remover temas e plugins não utilizados
- [ ] Instalar apenas plugins/temas de fontes confiáveis
- [ ] Manter core, temas e plugins sempre atualizados
- [ ] Verificar integridade do core com `wp core verify-checksums`
- [ ] Desativar editor de arquivos pelo painel (`DISALLOW_FILE_EDIT`)
- [ ] Evitar plugins desnecessários — preferir soluções via código

## 🧾 4. Segurança no wp-config.php
- [ ] Mover `wp-config.php` para uma pasta acima de `public_html` (se possível)
- [ ] Chaves de segurança únicas e atualizadas (https://api.wordpress.org/secret-key/1.1/salt/)
- [ ] Prefixo da tabela personalizado (ex: `wp8sd_`)
- [ ] Forçar SSL no painel (`FORCE_SSL_ADMIN`)

## 📁 5. Banco de Dados
- [ ] Usuário do banco com permissões mínimas
- [ ] Nome do banco não padrão (evitar `wordpress`)
- [ ] Backup automático diário do banco
- [ ] Monitoramento de alterações no banco

## 📬 6. Segurança nos E-mails
- [ ] Evitar função `mail()` — usar SMTP autenticado
- [ ] Usar plugin confiável de envio de e-mail (ex: WP Mail SMTP, QuicklyPHPMailer)
- [ ] Configurar SPF, DKIM e DMARC no DNS

## 📦 7. Backups e Logs
- [ ] Backup completo diário (arquivos + banco)
- [ ] Backup em nuvem (S3, Google Drive, etc)
- [ ] Ativar logs de erro e acesso
- [ ] Ativar logs de atividades (ex: Simple History)

## 🧪 8. Monitoramento e Testes
- [ ] Usar scanner de segurança (Wordfence, Sucuri, etc)
- [ ] Testes periódicos com WPScan CLI/API
- [ ] Receber alertas por e-mail sobre alterações

## 🧩 9. Plugins Recomendados
- [ ] 🔒 Wordfence Security ou iThemes Security
- [ ] 🔄 WPVivid Backup ou UpdraftPlus
- [ ] 🔐 WP 2FA (autenticação em duas etapas)
- [ ] 🕵️ Simple History (logs de atividades)

## 🧠 10. Boas Práticas Gerais
- [ ] Treinar equipe sobre phishing e boas práticas
- [ ] Nunca enviar senhas por e-mail
- [ ] Monitorar e excluir contas inativas
- [ ] Evitar temas/plugins nulled (piratas)
