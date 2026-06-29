# Azure-Projeto-3

# Azure SQL Managed Instance – Resumo, Anotações e Dicas de Estudo

## Visão Geral

A Azure SQL Managed Instance (MI) é um serviço PaaS (Platform as a Service) da Microsoft que oferece alta compatibilidade com o SQL Server tradicional, reduzindo a necessidade de gerenciamento de infraestrutura.

### Principais Benefícios
- Administração simplificada.
- Alta disponibilidade nativa.
- Backups automáticos.
- Escalabilidade de recursos.
- Integração com serviços Azure.
- Compatibilidade com aplicações SQL Server existentes.

---

# Pré-requisitos

Antes de criar uma Managed Instance:

- Possuir uma assinatura Azure ativa.
- Ter permissões adequadas:
  - SQL Managed Instance Contributor.
  - Ou permissão Microsoft.Sql/managedInstances/write.
- Utilizar Azure Portal, PowerShell ou Azure CLI.
- Planejar previamente rede virtual e sub-rede.

---

# Processo de Criação

## 1. Configurações Básicas

### Informações Obrigatórias

- Assinatura Azure.
- Grupo de Recursos.
- Nome da Instância.
- Região.
- Método de autenticação.
- Usuário administrador.
- Senha forte.

### Boas Práticas

✅ Utilizar autenticação Microsoft Entra (Azure AD) sempre que possível.

✅ Utilizar nomes padronizados para recursos.

✅ Escolher a região mais próxima dos usuários.

---

## 2. Computação e Armazenamento

### Camada de Serviço

#### General Purpose (Uso Geral)
Indicada para a maioria dos ambientes.

Vantagens:
- Menor custo.
- Boa performance.
- Ideal para aplicações corporativas comuns.

### Hardware

Recomendação:
- Standard Series (Gen5)

### vCores

Representam capacidade computacional.

Exemplos:
- 4 vCores → ambientes pequenos.
- 8 vCores → padrão.
- 16+ vCores → cargas pesadas.

### Armazenamento

Dimensionar considerando:
- Crescimento futuro.
- Índices.
- Backups.
- Logs.

---

# Rede

A Managed Instance exige uma sub-rede dedicada.

## Requisitos

### Virtual Network (VNet)

Pode ser:
- Nova.
- Existente.

### Sub-rede

Deve estar:
- Delegada para Microsoft.Sql/managedInstances.
- Configurada corretamente.

### Network Security Group (NSG)

Controla:
- Tráfego de entrada.
- Tráfego de saída.

### Route Table

Controla o roteamento da rede.

---

# Conectividade

## Endpoint Público

Por padrão:

❌ Desabilitado

### Quando habilitar

Somente quando necessário.

### Ambiente de Produção

Preferir:
- VPN.
- ExpressRoute.
- Redes privadas.

---

# Segurança

## Recomendações

### Autenticação

Preferir:
- Microsoft Entra ID

Evitar depender apenas de:
- SQL Login

### Senhas

Utilizar:
- 16+ caracteres.
- Letras maiúsculas.
- Letras minúsculas.
- Números.
- Caracteres especiais.

---

# Configurações Adicionais

## Collation

Importante em migrações.

Verificar no SQL Server origem:

```sql
SELECT SERVERPROPERTY(N'Collation')
```

## Fuso Horário

Configurar conforme a localização do negócio.

## Janela de Manutenção

Permite controlar quando atualizações ocorrerão.

### Boa prática

Agendar:
- Madrugada.
- Horários de menor utilização.

---

# Tags (Marcas)

Utilizar tags para governança.

Exemplos:

| Tag | Exemplo |
|------|----------|
| Owner | Marcos |
| Environment | Production |
| CostCenter | TI |
| Project | DataPlatform |

Benefícios:
- Controle financeiro.
- Organização.
- Automação.
- Governança.

---

# Monitoramento

Acompanhar a implantação através:

- Notifications.
- Deployment Center.
- Activity Log.
- Azure Monitor.

Observação:
A criação de uma Managed Instance pode levar bastante tempo.

---

# Criação de Banco de Dados

Após a criação da instância:

1. Abrir a Managed Instance.
2. Selecionar "Novo Banco de Dados".
3. Definir nome.
4. Escolher origem:
   - Banco vazio.
   - Restore de backup.
5. Revisar e criar.

---

# Recuperação da String de Conexão

Após a implantação:

1. Abrir a instância.
2. Acessar Overview.
3. Copiar o Host Name (FQDN).

Exemplo:

```text
minha-instancia.abc123.database.windows.net
```

Esse endereço será utilizado por:
- Aplicações.
- Ferramentas de BI.
- SSMS.
- Scripts.

---

# Dicas para Certificações e Estudos

## Conceitos Fundamentais

Estudar:

- Azure Resource Groups.
- Azure Virtual Networks.
- NSG.
- Route Tables.
- Azure Identity.
- Microsoft Entra ID.
- Azure Monitor.
- Backup e Recovery.

## Serviços Relacionados

- Azure SQL Database.
- Azure SQL Managed Instance.
- SQL Server on Azure VM.
- Azure Storage.
- Azure Backup.
- Azure Key Vault.

---

# Comparação Rápida

| Serviço | Gerenciamento | Compatibilidade SQL Server |
|-----------|--------------|----------------------------|
| SQL Database | Baixo | Média |
| SQL Managed Instance | Baixo | Alta |
| SQL Server VM | Alto | Total |

---

# Erros Comuns

❌ Sub-rede não delegada.

❌ Regras NSG bloqueando tráfego.

❌ Região sem suporte.

❌ Permissões insuficientes.

❌ Endpoint público habilitado sem proteção.

❌ Dimensionamento inadequado de vCores.

---

# Checklist de Implementação

## Planejamento

- [ ] Definir região.
- [ ] Definir vCores.
- [ ] Definir armazenamento.
- [ ] Criar Resource Group.

## Rede

- [ ] Criar VNet.
- [ ] Criar Sub-rede.
- [ ] Delegar sub-rede.
- [ ] Configurar NSG.
- [ ] Configurar rotas.

## Segurança

- [ ] Definir administrador.
- [ ] Habilitar Entra ID.
- [ ] Revisar regras de acesso.

## Governança

- [ ] Aplicar Tags.
- [ ] Configurar monitoramento.
- [ ] Definir política de manutenção.

## Pós-Implantação

- [ ] Criar banco.
- [ ] Testar conexão.
- [ ] Configurar backup.
- [ ] Documentar ambiente.

---

# Resumo Final

A Azure SQL Managed Instance é a melhor opção para organizações que desejam migrar bancos SQL Server para a nuvem com alta compatibilidade e menor esforço operacional. O sucesso da implementação depende principalmente do planejamento da rede, segurança, governança e dimensionamento adequado dos recursos.
