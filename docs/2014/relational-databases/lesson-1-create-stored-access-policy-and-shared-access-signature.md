---
title: Lição 2. Criar uma política no contêiner e gerar uma chave de assinatura de acesso compartilhado (SAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 41674d9d-8132-4bff-be4d-85a861419f3d
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c5313872497e120ebfce452547f755f61ba567e4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116906"
---
# <a name="lesson-2-create-a-policy-on-container-and-generate-a-shared-access-signature-sas-key"></a>Lição 2. Criar uma política no contêiner e gerenciar uma chave SAS (assinatura de acesso compartilhado)
  Nesta lição, você aprenderá a criar uma política no contêiner do Blob e também gerará uma chave de SAS.  
  
 Uma política de acesso armazenado fornece um nível de controle adicional sobre assinaturas de acesso compartilhado no lado do servidor. Uma assinatura de acesso compartilhado é um URI que concede direitos de acesso restrito a contêineres, blobs, filas e tabelas. Ao usar esse novo aprimoramento, você precisa criar uma política em um contêiner com direitos de leitura, gravação e lista.  
  
 Você pode criar uma política e uma assinatura de acesso compartilhado usando um destes métodos:  
  
-   Operações da API de REST do Windows Azure: [criar contêiner](https://msdn.microsoft.com/library/azure/dd179468.aspx), [definir ACL do contêiner](https://msdn.microsoft.com/library/azure/dd179391.aspx), e [obter ACL do contêiner](https://msdn.microsoft.com/library/azure/dd179469.aspx).  
  
-   [GetSharedAccessSignature método](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storageclient.cloudblobcontainer.getsharedaccesssignature.aspx) nas janelas do SDK do Azure.  
  
    ```  
  
       string signature = blob.GetSharedAccessSignature(new SharedAccessPolicy()   
        {   
            // Specify the expiration time for the signature.   
            SharedAccessExpiryTime = DateTime.Now.Years(1),   
            // Specify the permissions granted by the signature.    
            Permissions = SharedAccessPermissions.Write | SharedAccessPermissions.Read   
        });  
  
    ```  
  
-   Ferramenta de um pesquisador do Windows Azure de terceiros, como [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/).  
  
 **Próxima lição:**  
  
 [Lição 3: criar uma credencial do SQL Server](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)  
  
  