---
title: Instalar o SSMA para cliente DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 3ae2a470-6afd-4512-b6d1-fcbe6afe88ad
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1d479c8f7de1c9d7463e57f37f9e8588c9bc68b6
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51666495"
---
# <a name="installing-ssma-for-db2-client-db2tosql"></a>Instalar o SSMA para cliente DB2 (DB2ToSQL)
O cliente SSMA consiste em arquivos de programa que executam as seguintes tarefas:  
  
-   Conecte-se a um banco de dados do DB2.  
  
-   Conectar-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Converter objetos de banco de dados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe.  
  
-   Carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Este tópico fornece os pré-requisitos de instalação e as instruções para instalar o SSMA.  
  
## <a name="prerequisites"></a>Prerequisites  
O SSMA é projetado para trabalhar com o DB2 em z/OS versão 9.0 e 10.0 ou DB2 em LUW versão 9,8 e 10.1 ou versões posteriores e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014.  
  
Antes de instalar o SSMA, certifique-se de que o computador atende aos seguintes requisitos:  
  
-   Windows 7 ou versões posteriores, ou Windows Server 2008 ou versões posteriores.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 ou posterior.  
  
-   O [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versão 4.0 ou posterior. O [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versão 4.0 está disponível no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mídia do produto. Você também pode obtê-lo do [.NET Framework Developer Center](https://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   Provedor Microsoft OLEDB para DB2 versão 5 ou uma versão posterior e a conectividade com os bancos de dados do DB2 que você deseja migrar.  
  
-   Acesso a e permissões suficientes no computador que hospeda a instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados do SQL Azure em que será migrado dados e objetos de banco de dados. Para obter mais informações, consulte [conectando ao SQL Server &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md).  
  
-   4 GB de RAM são recomendados.  
  
## <a name="microsoft-oledb-provider-for-db2"></a>Provedor Microsoft OLEDB para DB2  
Para baixar o provedor OLE DB para DB2 versão 5.0, vá para [Microsoft® SQL Server® 2014 Feature Pack](https://www.microsoft.com/download/details.aspx?id=42295).  
  
O SSMA é um download da Web. Para baixar a versão mais recente, consulte o [página de download do SQL Server Migration Assistant](https://aka.ms/ssmafordb2).  
  
Depois de baixar a versão mais recente, você deve extrair os arquivos de instalação antes de instalar o SSMA.  
  
**Para instalar o cliente SSMA**  
  
1.  Clique duas vezes o SSMA para DB2 *n*. Install.exe, onde *n* é o número de compilação.  
  
2.  Na página de boas-vinda, clique em **próxima**.  
  
    Se você não tiver os pré-requisitos instalados, será exibida uma mensagem que indica que você deve primeiro instalar os componentes necessários. Certifique-se de que você instalou todos os pré-requisitos e, em seguida, execute o programa de instalação novamente.  
  
3.  Leia o contrato de licença de usuário final. Se você concordar, marque **aceito os termos do contrato de licença**e, em seguida, clique em **próxima**.  
  
4.  Na página Escolha o tipo de instalação, clique em **típica**.  
  
5.  Clique em **Instalar**.  
  
> [!IMPORTANT]  
> 1.  Desinstale todas as versões anteriores do SSMA para DB2 antes de instalar a nova versão.  
  
O local de instalação padrão é C:\Program Files\Microsoft SQL Server Migration Assistant for DB2.  
  
## <a name="see-also"></a>Consulte também  
[Instalar os componentes do SSMA no SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
[Bancos de dados do DB2 migrando para o SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
