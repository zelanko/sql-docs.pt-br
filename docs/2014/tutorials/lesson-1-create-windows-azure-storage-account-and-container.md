---
title: 'Lição 1: criar uma conta de armazenamento do Azure e o contêiner | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: efdbd930-cde5-41b0-90ad-58a6cc68dddc
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: fbe773b8b8115cafc20bb60e962bfb42c9821636
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75253497"
---
# <a name="lesson-1-create-azure-storage-account-and-container"></a>Lição 1: criar uma conta de armazenamento do Azure e um contêiner
  Antes de poder começar a armazenar SQL Server arquivos de dados no armazenamento do Azure, você deve primeiro criar uma conta de armazenamento do Azure e um contêiner de BLOB e uma assinatura de acesso compartilhado. A lição 1 orienta você pelas etapas de fazer logon na Portal de Gerenciamento do Azure, criar uma conta de armazenamento, um contêiner de BLOB e uma assinatura de acesso compartilhado.  
  
 Por padrão, somente o proprietário da conta de armazenamento pode acessar blobs, tabelas e filas nessa conta. Para acessar esses recursos usando esse novo aprimoramento do SQL Server sem compartilhar a chave de acesso da conta de armazenamento, será necessário fazer o seguinte:  
  
-   Defina as permissões do contêiner como privadas.  
  
-   Crie uma assinatura de acesso compartilhado. Ela permitirá que você delegue acesso restrito a um contêiner, um blob, uma tabela ou um recurso de fila, especificando o intervalo no qual os recursos estarão disponíveis e as permissões que um cliente terá nesse intervalo.  
  
-   Use uma política de acesso armazenado para gerenciar assinaturas de acesso compartilhado para um contêiner ou seus blobs. A política de acesso armazenado oferece a você uma medida adicional de controle sobre suas assinaturas de acesso compartilhado, além de fornecer um meio simples de revogá-los.  
  
 Para saber mais, confira [Gerenciar o acesso aos recursos de Armazenamento do Azure](https://msdn.microsoft.com/library/windowsazure/ee393343.aspx).  
  
## <a name="create-storage-account"></a>Criar conta de armazenamento  
 Para criar uma conta de armazenamento no Portal de Gerenciamento do Azure, siga estas etapas:  
  
1.  Faça logon no [Azure portal de gerenciamento](https://manage.windowsazure.com) usando sua conta. Se você não tiver uma conta do Azure, visite [Avaliação gratuita do Azure](https://www.windowsazure.com/pricing/free-trial/).  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-1.gif "SQL 14 CTP2")  
  
2.  Use as instruções passo a passo para [criar uma conta de armazenamento](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/). Observe que ao criar uma conta de armazenamento a ser usada para o SQL Server arquivos de dados no recurso do Azure, você deve desmarcar ou desabilitar a replicação geográfica. Isso acontece porque a ordem de gravação não é garantida para vários blobs que participam da replicação geográfica. Se uma conta de armazenamento for replicada geograficamente e a recuperação for necessária, ocorrerá um dano.  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-2.gif "SQL 14 CTP2")  
  
## <a name="create-a-blob-container"></a>Criar um contêiner de Blob  
 No Azure, um contêiner fornece um agrupamento de um conjunto de BLOBs. Todos os blobs devem ter um contêiner. Uma conta de armazenamento pode conter um número ilimitado de contêineres, mas deve ter pelo menos um contêiner. Um contêiner pode armazenar um número ilimitado de blobs. Para obter informações mais atualizadas sobre os limites de tamanho de armazenamento, consulte [como usar o serviço de armazenamento de BLOBs do Azure no .net](https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/).  
  
 Para criar um contêiner no Azure, siga estas etapas:  
  
1.  Faça logon no [Portal de Gerenciamento do Azure](https://manage.windowsazure.com).  
  
2.  Selecione a conta de armazenamento, clique na guia **contêineres** e clique em **Adicionar contêiner** na parte inferior da tela, que abre uma nova caixa de diálogo.  
  
3.  Insira um nome do contêiner.  
  
4.  Selecione **privado** para **tipo de acesso**. Quando você define o acesso como particular, os dados de contêiner e BLOB podem ser lidos somente pelo proprietário da conta do Azure.  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-4.gif "SQL 14 CTP2")  
  
> [!NOTE]  
>  Para criar uma contêiner de modo programático, você também poderá usar as APIs REST. Para obter mais informações, consulte [criar contêiner](https://msdn.microsoft.com/library/windowsazure/dd179468.aspx) e também [referência da API REST dos serviços de armazenamento do Azure](https://msdn.microsoft.com/library/windowsazure/dd179355.aspx).  
  
 **Próxima lição:**  
  
 [Lição 2. Criar uma política no contêiner e gerar uma assinatura de acesso compartilhado &#40;chave de&#41; SAS](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)  
  
