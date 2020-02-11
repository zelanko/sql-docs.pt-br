---
title: 'Lição 1: criar objetos de armazenamento do Azure | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 74edd1fd-ab00-46f7-9e29-7ba3f1a446c5
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 53fcba3401a6798fb865613470ba78aa05e9b6dd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70176109"
---
# <a name="lesson-1-create-azure-storage-objects"></a>Lição 1: Criar objetos de Armazenamento do Azure
  Para que você possa criar backups do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no armazenamento em nuvem, primeiro crie uma conta de armazenamento e, depois, um contêiner de blob. A lição 1 orienta você pelas etapas de fazer logon na Portal de Gerenciamento do Azure, criando uma conta de armazenamento e um contêiner de BLOB.  
  
## <a name="create-a-storage-account"></a>Criar uma conta de armazenamento  
 Para criar uma conta de armazenamento do Portal de Gerenciamento do Azure, use as seguintes etapas:  
  
1.  Faça logon no portal de gerenciamento do Azure usando sua conta. Se você não tiver uma conta do Azure, [visite avaliação gratuita de 3 meses do Azure](https://go.microsoft.com/fwlink/?LinkId=271927).  
  
     ![Tela de logon do Azure](../../2014/tutorials/media/windowazurelogin-backuptocloud.gif "Tela de logon do Azure")  
  
2.  Use as instruções passo a passo detalhadas [aqui](https://go.microsoft.com/fwlink/?LinkId=271926)para criar uma conta de armazenamento.  
  
3.  Procure a conta de armazenamento que você criou na etapa anterior. Na parte inferior central da página da Web, clique em **gerenciar chaves**. As informações da conta serão exibidas. Copie o nome da conta de armazenamento e as chaves de acesso. Essas informações são necessárias para criar credenciais armazenadas do SQL. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usará essas informações para acessar a conta de armazenamento e criar backups.  
  
     ![Captura de tela de chaves de conta de armazenamento do Azure](../../2014/tutorials/media/manageaccesskeys-backuptocloud.gif "Captura de tela de chaves de conta de armazenamento do Azure")  
  
    > [!NOTE]  
    >  Você também pode criar uma conta de armazenamento de modo programático usando APIs REST. Para obter mais informações, consulte [criar conta de armazenamento](https://go.microsoft.com/fwlink/?LinkId=271928).  
  
### <a name="create-a-blob-container"></a>Crie um contêiner de blob  
 Um contêiner fornece um agrupamento de conjunto de blobs. Todos os blobs devem estar em um contêiner. Uma conta pode conter um número ilimitado de contêineres, mas deve ter pelo menos um contêiner. Um contêiner pode armazenar um número ilimitado de blobs.  
  
 Para criar um contêiner, execute as seguintes etapas:  
  
1.  Selecione a conta de armazenamento, clique na guia **contêineres** e clique em **Adicionar contêiner** na parte inferior da tela que abre uma nova caixa de diálogo.  
  
     ![Criando um contêiner no Portal de Gerenciamento](../../2014/tutorials/media/backuptocloud.gif "Criando um contêiner no Portal de Gerenciamento")  
  
2.  Insira um nome do contêiner. Anote o nome de contêiner que você especificou. Essas informações são usadas na URL (caminho para o arquivo de backup) nas instruções T-SQL das lições 3 e 4.  
  
3.  Selecione privado para **tipo de acesso**. É recomendável criar contêiner privados para proteger os arquivos de backup.  
  
     ![Criando um novo contêiner de blob.](../../2014/tutorials/media/backuptocloud-newblobcontainer.gif "Criando um novo contêiner de blob.")  
  
    > [!NOTE]  
    >  A autenticação na conta de armazenamento é necessária para o backup e a restauração do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], mesmo se você optar por criar um contêiner público.  
    >   
    >  Você também pode criar uma contêiner de modo programático usando APIs REST. Para obter mais informações, consulte [criar contêiner](https://go.microsoft.com/fwlink/?LinkId=271946).  
  
### <a name="next-lesson"></a>Próxima lição  
 [Lição 2: criar uma credencial de SQL Server](../../2014/tutorials/lesson-2-create-a-sql-server-credential.md).  
  
  
