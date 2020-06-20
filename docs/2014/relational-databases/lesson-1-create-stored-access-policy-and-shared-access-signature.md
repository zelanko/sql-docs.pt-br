---
title: Lição 2. Criar uma política no contêiner e gerar uma chave de assinatura de acesso compartilhado (SAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 41674d9d-8132-4bff-be4d-85a861419f3d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 73056d9d70b66a519074e06d4e9420173fb1b190
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85025051"
---
# <a name="lesson-2-create-a-policy-on-container-and-generate-a-shared-access-signature-sas-key"></a>Lição 2. Criar uma política no contêiner e gerenciar uma chave SAS (assinatura de acesso compartilhado)
  Nesta lição, você aprenderá a criar uma política no contêiner do Blob e também gerará uma chave de SAS.  
  
 Uma política de acesso armazenado fornece um nível de controle adicional sobre assinaturas de acesso compartilhado no lado do servidor. Uma assinatura de acesso compartilhado é um URI que concede direitos de acesso restrito a contêineres, blobs, filas e tabelas. Ao usar esse novo aprimoramento, você precisa criar uma política em um contêiner com direitos de leitura, gravação e lista.  
  
 Você pode criar uma política e uma assinatura de acesso compartilhado usando um destes métodos:  
  
-   Operações da API REST do Azure: [criar contêiner](https://msdn.microsoft.com/library/azure/dd179468.aspx), [definir ACL de contêiner](https://msdn.microsoft.com/library/azure/dd179391.aspx)e [obter ACL de contêiner](https://msdn.microsoft.com/library/azure/dd179469.aspx).  
  
-   [Método CloudBlobContainer. GetSharedAccessSignature](https://docs.microsoft.com/dotnet/api/microsoft.azure.storage.blob.cloudblobcontainer.getsharedaccesssignature) no SDK do Azure.  
  
    ```  
  
       string signature = blob.GetSharedAccessSignature(new SharedAccessPolicy()   
        {   
            // Specify the expiration time for the signature.   
            SharedAccessExpiryTime = DateTime.Now.Years(1),   
            // Specify the permissions granted by the signature.    
            Permissions = SharedAccessPermissions.Write | SharedAccessPermissions.Read   
        });  
  
    ```  
  
-   Uma ferramenta de terceiros do Azure Explorer, como [Gerenciador de armazenamento do Azure](https://azurestorageexplorer.codeplex.com/).  
  
 **Próxima lição:**  
  
 [Lição 3: Criar uma credencial do SQL Server](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)  
  
