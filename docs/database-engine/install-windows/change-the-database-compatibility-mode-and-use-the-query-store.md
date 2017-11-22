---
title: "Alterar o modo de compatibilidade do banco de dados e usar o Repositório de Consultas | Microsoft Docs"
ms.custom: 
ms.date: 07/21/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology: setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- query plans [SQL Server], migrating
- upgrading SQL Server, migrating query plans
- plan guides [SQL Server], migrating query plans
ms.assetid: 7e02a137-6867-4f6a-a45a-2b02674f7e65
caps.latest.revision: "19"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: a230544eba53d9b506aae4bce6feb019820550e6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="change-the-database-compatibility-mode-and-use-the-query-store"></a>Alterar o modo de compatibilidade do banco de dados e usar o repositório de consultas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

No SQL Server 2016 e SQL Server 2017, algumas alterações são habilitadas somente quando o nível de DATABASE_COMPATIBILITY de um banco de dados é alterado. Isso foi feito por vários motivos:  
  
- Uma vez que a atualização é uma operação unidirecional (não é possível fazer downgrade do formato de arquivo), há valor em separar a habilitação de novos recursos para uma operação separada dentro do banco de dados.  É possível reverter uma configuração para um nível de DATABASE_COMPATIBILITY anterior.  O novo modelo reduz o número de itens que devem ocorrer durante uma janela de interrupção.  
  
- Alterações no processador de consulta podem ter efeitos complexos.  Até mesmo uma alteração “boa” para o sistema pode ser ótima para a maioria dos clientes, assim como pode causar uma regressão inaceitável em uma consulta importante para outros.  Separar essa lógica do processo de atualização permite que determinados recursos, assim como o Repositório de Consultas, realizem rapidamente a mitigação das escolhas de plano ou até mesmo evitem-nas completamente em servidores de produção.  
  
> [!NOTE]  
>  Se o nível de compatibilidade de um banco de dados de usuário era 100 ou mais alto antes da atualização, ele permanecerá o mesmo depois da atualização. Se o nível de compatibilidade era 90 antes da atualização, no banco de dados atualizado, o nível de compatibilidade será definido como 100, que é o nível de compatibilidade mais baixo com suporte no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Os níveis de compatibilidade dos bancos de dados tempdb, model, msdb e Resource são definidos para o nível de compatibilidade atual após o upgrade. O banco de dados do sistema mestre retém o nível de compatibilidade anterior ao upgrade. 
  
 O processo de atualização para habilitar a nova funcionalidade do processador de consulta está relacionado ao modelo de manutenção pós-lançamento do produto.  Algumas dessas correções são liberadas sob o sinalizador de rastreamento 4199.  Clientes que precisam de correções podem optar por aceitar essas correções sem causar regressões inesperadas para outros clientes.  O modelo de manutenção pós-lançamento para hotfixes do processador de consulta é documentado [aqui](https://support.microsoft.com/en-us/kb/974006). A partir do SQL Server 2016, a mudança para um novo nível de compatibilidade implica no sinalizador de rastreamento 4199 não ser mais necessário, porque essas correções agora estão habilitadas por padrão no último modo de compatibilidade.  Portanto, como parte do processo de atualização, é importante validar que o 4199 não está habilitado quando o processo de atualização for concluído.  
  
 O fluxo de trabalho recomendado para atualizar o processador de consultas para a versão mais recente do código é:  
  
1.  Atualizar um banco de dados para o SQL Server 2016 sem alterar o nível de compatibilidade do banco de dados (mantê-lo no nível anterior)  
  
2.  Habilite o repositório de consultas no banco de dados. Para obter mais informações sobre a habilitação e o uso do repositório de consultas, consulte [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md).  
  
3.  Aguarde tempo suficiente para coletar dados representativos da carga de trabalho.  
  
4.  Altere o nível de compatibilidade do banco de dados para o nível de compatibilidade atual. 

   >[!NOTE]
   >O último nível de compatibilidade depende da versão do SQL Server.
   >- SQL Server 2016: 130
   >- SQL Server 2017: 140

5. Usando o SQL Server Management Studio, avalie se há regressões de desempenho em consultas específicas após a alteração do nível de compatibilidade.
  
6.  Nos casos em que há regressões, force o plano anterior no repositório de consultas.  
  
7.  Se houver planos de consulta que falham ao forçar ou se o desempenho ainda for insuficiente, considere reverter o nível de compatibilidade à configuração anterior e então contatar Suporte ao Cliente Microsoft.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir ou alterar o nível de compatibilidade de um banco de dados](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)  
  
  
