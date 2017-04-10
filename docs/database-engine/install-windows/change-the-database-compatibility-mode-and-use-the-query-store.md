---
title: "Alterar o modo de compatibilidade do banco de dados e usar o reposit&#243;rio de consultas | Microsoft Docs"
ms.custom: ""
ms.date: "09/22/2015"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "planos de consulta [SQL Server], migrando"
  - "atualizando o SQL Server, migrando planos de consulta"
  - "guias de plano [SQL Server], migrando planos de consulta"
ms.assetid: 7e02a137-6867-4f6a-a45a-2b02674f7e65
caps.latest.revision: 19
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 17
---
# Alterar o modo de compatibilidade do banco de dados e usar o reposit&#243;rio de consultas
  No SQL Server 2016, algumas alterações são habilitadas somente quando o nível de DATABASE_COMPATIBILITY para um banco de dados é alterado para 130.  Isso foi feito por vários motivos:  
  
-   Uma vez que a atualização é uma operação unidirecional (não é possível fazer downgrade do formato de arquivo), há valor em separar a habilitação de novos recursos para uma operação separada dentro do banco de dados.  É possível reverter uma configuração para um nível de DATABASE_COMPATIBILITY anterior.  O novo modelo reduz o número de itens que devem ocorrer durante uma janela de interrupção.  
  
-   Alterações no processador de consulta podem ter efeitos complexos.  Até mesmo uma alteração "boa" para o sistema pode ser ótima para a maioria dos clientes, assim como pode causar uma regressão inaceitável em uma consulta importante em outro lugar.  Separar essa lógica do processo de atualização permite que determinados recursos, assim como o Repositório de Consultas, realizem rapidamente a mitigação das escolhas de plano ou até mesmo evitem-nas completamente em servidores de produção.  
  
> [!NOTE]  
>  Se o nível de compatibilidade de um banco de dados de usuário era 100 ou mais alto antes da atualização, ele permanecerá o mesmo depois da atualização. Se o nível de compatibilidade era 90 antes da atualização, no banco de dados atualizado, o nível de compatibilidade será definido como 100, que é o nível de compatibilidade mais baixo com suporte no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 O processo de atualização para habilitar a nova funcionalidade do processador de consulta está relacionado ao modelo de manutenção pós-lançamento do produto.  Algumas dessas correções são liberadas sob o sinalizador de rastreamento 4199.  Clientes que precisam de correções podem optar por aceitar essas correções sem causar regressões inesperadas para outros clientes.  O modelo de manutenção pós-lançamento para hotfixes do processador de consulta é documentado [aqui](https://support.microsoft.com/en-us/kb/974006). Do SQL Server 2016 em diante, mudar para um novo nível de compatibilidade implica que o sinalizador de rastreamento 4199 não é mais necessário, porque essas correções agora estão habilitadas por padrão no modo de compatibilidade mais recente (130).  Portanto, como parte do processo de atualização, é importante validar que o 4199 não está habilitado quando o processo de atualização for concluído.  
  
 O fluxo de trabalho recomendado para atualizar o processador de consultas para a versão mais recente do código é:  
  
1.  Atualizar um banco de dados para o SQL Server 2016 sem alterar o nível de compatibilidade do banco de dados (mantê-lo no nível anterior)  
  
2.  Habilite o repositório de consultas no banco de dados. Para obter mais informações sobre a habilitação e o uso do repositório de consultas, consulte [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md).  
  
3.  Aguarde tempo suficiente para coletar dados representativos da carga de trabalho.  
  
4.  Alterar o nível de compatibilidade do banco de dados para 130  
  
5.  Usando o SQL Server Management Studio, avalie se há regressões de desempenho em consultas específicas após a alteração do nível de compatibilidade  
  
6.  Nos casos em que há regressões, force o plano anterior no repositório de consultas.  
  
7.  Se houver planos de consulta que falham ao forçar ou se o desempenho ainda for insuficiente, considere reverter o nível de compatibilidade à configuração anterior e então contatar Suporte ao Cliente Microsoft.  
  
## Consulte também  
 [Exibir ou alterar o nível de compatibilidade de um banco de dados](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)  
  
  