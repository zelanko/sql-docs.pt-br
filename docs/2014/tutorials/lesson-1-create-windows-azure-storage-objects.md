---
title: 'Lição 1: Criar objetos de armazenamento do Azure do Windows | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 74edd1fd-ab00-46f7-9e29-7ba3f1a446c5
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 916139aa9f5e30581abc29421cafb2bb5eb06ee7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009471"
---
# <a name="lesson-1-create-windows-azure-storage-objects"></a>Lição 1: Criar objetos de armazenamento do Windows Azure
  Para que você possa criar backups do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no armazenamento em nuvem, primeiro crie uma conta de armazenamento e, depois, um contêiner de blob. A lição 1 conduzirá você pelas etapas do registro em log no portal de gerenciamento do Windows Azure, criando uma conta de armazenamento e um contêiner de blob.  
  
## <a name="create-a-storage-account"></a>Criar uma conta de armazenamento  
 Para criar uma conta de armazenamento no portal de gerenciamento do Windows Azure, execute as seguintes etapas:  
  
1.  Entre ao portal de gerenciamento do Windows Azure usando sua conta. Se você não tiver uma conta do Windows Azure, [visite avaliação gratuita de 3 meses do Windows Azure](http://go.microsoft.com/fwlink/?LinkId=271927).  
  
     ![Tela de logon do Azure Windows](../../2014/tutorials/media/windowazurelogin-backuptocloud.gif "tela de logon do Azure do Windows")  
  
2.  Use as instruções passo a passo detalhadas [aqui](http://go.microsoft.com/fwlink/?LinkId=271926), para criar uma conta de armazenamento.  
  
3.  Procure a conta de armazenamento que você criou na etapa anterior. Na parte inferior central da página da web, clique em **gerenciar chaves**. As informações da conta serão exibidas. Copie o nome da conta de armazenamento e as chaves de acesso. Essas informações são necessárias para criar credenciais armazenadas do SQL. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usará essas informações para acessar a conta de armazenamento e criar backups.  
  
     ![Captura de tela de chaves de conta de armazenamento do Windows Azure](../../2014/tutorials/media/manageaccesskeys-backuptocloud.gif "captura de tela de chaves de conta de armazenamento do Windows Azure")  
  
    > [!NOTE]  
    >  Você também pode criar uma conta de armazenamento de modo programático usando APIs REST. Para obter mais informações, consulte [criar conta de armazenamento](http://go.microsoft.com/fwlink/?LinkId=271928).  
  
### <a name="create-a-blob-container"></a>Crie um contêiner de blob  
 Um contêiner fornece um agrupamento de conjunto de blobs. Todos os blobs devem estar em um contêiner. Uma conta pode conter um número ilimitado de contêineres, mas deve ter pelo menos um contêiner. Um contêiner pode armazenar um número ilimitado de blobs.  
  
 Para criar um contêiner, execute as seguintes etapas:  
  
1.  Selecione a conta de armazenamento, clique o **CONTÊINERES** guia e clique em **adicionar CONTÊINER** na parte inferior da tela que abre uma nova caixa de diálogo.  
  
     ![Criando um contêiner no Portal de gerenciamento](../../2014/tutorials/media/backuptocloud.gif "criar um contêiner no Portal de gerenciamento")  
  
2.  Insira um nome do contêiner. Anote o nome de contêiner que você especificou. Essas informações são usadas na URL (caminho para o arquivo de backup) nas instruções T-SQL das lições 3 e 4.  
  
3.  Selecione privado em **acessar tipo**. É recomendável criar contêiner privados para proteger os arquivos de backup.  
  
     ![Criando um novo contêiner de blob](../../2014/tutorials/media/backuptocloud-newblobcontainer.gif "criando um novo contêiner de blob")  
  
    > [!NOTE]  
    >  A autenticação na conta de armazenamento é necessária para o backup e a restauração do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], mesmo se você optar por criar um contêiner público.  
    >   
    >  Você também pode criar uma contêiner de modo programático usando APIs REST. Para obter mais informações, consulte [criar contêiner](http://go.microsoft.com/fwlink/?LinkId=271946).  
  
### <a name="next-lesson"></a>Próxima lição  
 [Lição 2: Criar uma credencial do SQL Server](../../2014/tutorials/lesson-2-create-a-sql-server-credential.md).  
  
  