---
title: Gerar Script SQL (objetos de replicação) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.generatesqlscript.f1
helpviewer_keywords:
- Generate SQL Script dialog box
ms.assetid: b7ccc34e-1c22-44b8-8eb5-f6423af3164e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 7fbe5d78e911f526f9006acee3c9f9842ec2d5e2
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768565"
---
# <a name="generate-sql-script-replication-objects"></a>Gerar Script SQL (objetos de replicação)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Um script de replicação contém os procedimentos armazenados do sistema [!INCLUDE[tsql](../../includes/tsql-md.md)] necessários para implementar os componentes de replicação com scripts, como uma publicação ou assinatura. Todos os componentes de replicação em uma topologia devem ser incluídos no script como parte de um plano de recuperação de desastre  e os scripts também podem ser usados para automatizar tarefas repetitivas. A replicação oferece duas caixas de diálogo para scripts de objetos de replicação:  
  
-   **Generate SQL Script**, which is available from the context menu of the **Replication** folder and all subfolders in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Essa caixa de diálogo permite scripts de todos os objetos de replicação em uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Gerar Script SQL \<ObjectName>** disponível no menu de contexto para publicações e assinaturas. Essa caixa de diálogo permite script de objetos individuais.  
  
 Essas caixas de diálogo fazem scripts de objetos em uma instância única do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; elas não conectam com outras instâncias para script de objetos relacionados.  
  
## <a name="generate-sql-script-options"></a>Opções Generate SQL Script  
 **Propriedades do Distribuidor**  
 Selecione para script de procedimentos armazenados para: habilitar ou desabilitar o Distribuidor; adicionar ou descartar Publicadores associados com o Distribuidor e criar ou descartar o banco de dados de distribuição.  
  
 **Publicações nestas fontes de dados**  
 Selecione para script de procedimentos armazenados para: habilitar ou desabilitar publicação e criar ou descartar publicações, artigos, assinaturas push e trabalhos de replicação.  
  
 **Publicações nestas fontes de dados**  
 Selecione para escrever um script de procedimentos armazenados para criar ou descartar assinaturas pull e trabalhos de replicação.  
  
 **Criar ou habilitar os componentes** e **Descartar ou desabilitar os componentes**  
 Especifique se o script deve incluir comandos para criação ou remoção de um objeto de replicação. A[!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda usar a caixa de diálogo para criar um conjunto de scripts para habilitar e desabilitar componentes.  
  
 **Trabalhos de replicação**  
 Selecione para script de trabalhos de replicação além de chamadas de procedimento armazenado. Essa opção só está disponível ao efetuar script de um Distribuidor.  
  
 Procedimentos armazenados de replicação criam os trabalhos necessários quando são executados, portanto, não é necessário selecionar essa opção. No entanto, pode ser útil ter um registro dos trabalhos criados, caso seja necessário recriar um trabalho individual.  
  
## <a name="generate-sql-script-objectname-options"></a>Opções Gerar Script SQL \<ObjectName>  
 **Criar ou habilitar os componentes** e **Descartar ou desabilitar os componentes**  
 Especifique se o script deve incluir comandos para criação ou remoção de um objeto de replicação. A[!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda usar a caixa de diálogo para, criando um conjunto de scripts para habilitar e desabilitar componentes.  
  
 **Trabalhos de replicação**  
 Essa opção só está disponível na caixa de diálogo **Gerar Script SQL** .  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação de script](../../relational-databases/replication/scripting-replication.md)  
  
  
