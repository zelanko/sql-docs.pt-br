---
title: Conectar-se a uma Assinatura do Microsoft Azure | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cca5a270-643f-4677-8802-98464f19f82a
caps.latest.revision: 4
author: dagiro
ms.author: v-dagir
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6db65c242dc6dd9fd1c6c910d583d026f45422c1
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-a-microsoft-azure-subscription"></a>Conectar-se a uma Assinatura do Microsoft Azure
Use **Conectar-se a uma Assinatura da Microsoft** para registrar um contêiner de blobs do Azure existente na instância do SQL Server.  A caixa de diálogo criará uma assinatura de acesso compartilhado e uma política de acesso armazenado em um contêiner de blobs do Azure e, em seguida, criará uma Credencial do SQL Server.  Essa caixa de diálogo é exibida ao usar a tarefa Fazer Backup ou Restaurar do SQL Server Management Studio e a operação envolve um dispositivo URL.

## <a name="limitation"></a>Limitação
A opção**Conectar-se a uma Assinatura da Microsoft** só funcionará com uma Conta do Armazenamento do Azure criada por meio do modelo de implantação do Gerenciamento de Serviço (Clássico).  Para obter mais informações sobre os modelos de implantação do Azure, veja [Azure Resource Manager versus implantação clássica](https://azure.microsoft.com/en-us/documentation/articles/resource-manager-deployment-model/).

## <a name="options"></a>Opções
**Entrar**     
Entre com a conta do Azure apropriada.

**Selecionar uma assinatura para usar**      
Selecione a assinatura desejada na lista suspensa.

**Selecionar Conta de Armazenamento**  
Selecione a conta de armazenamento desejada na lista suspensa.

**Selecionar Contêiner de Blobs**   
Selecione o contêiner de blobs desejado na lista suspensa.

**Expiração da Política de Acesso Compartilhado**   
A política de acesso compartilhado expirará na data especificada.  A data de expiração padrão é de um ano após a criação.  Modifique a data conforme desejado.

**Assinatura de Acesso Compartilhado Gerada**   
A caixa de texto avançado exibirá a assinatura de acesso compartilhado gerada.

**Criar Credencial**   
Esse botão gerará uma política de acesso armazenado e uma assinatura de acesso compartilhado e, em seguida, criará uma credencial do SQL Server.

