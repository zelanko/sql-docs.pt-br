---
title: Instalando o SSMA para cliente DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 3ae2a470-6afd-4512-b6d1-fcbe6afe88ad
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d976466251d49f85074864ca39a034a988cbff4f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="installing-ssma-for-db2-client-db2tosql"></a>Instalando o SSMA para cliente DB2 (DB2ToSQL)
O cliente do SSMA consiste em arquivos de programas, executam as seguintes tarefas:  
  
-   Conecte-se a um banco de dados do DB2.  
  
-   Conectar-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Converter objetos de banco de dados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxe.  
  
-   Carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Este tópico fornece os pré-requisitos de instalação e instruções de instalação do SSMA.  
  
## <a name="prerequisites"></a>Prerequisites  
O SSMA é projetado para trabalhar com o DB2 em z/OS versão 9.0 e 10.0 ou DB2 em LUW versão 9,8 e 10.1 ou versões posteriores e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014.  
  
Antes de instalar o SSMA, certifique-se de que o computador atende aos seguintes requisitos:  
  
-   Windows 7 ou versões posteriores, ou Windows Server 2008 ou versões posteriores.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 ou posterior.  
  
-   O [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versão 4.0 ou posterior. O [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versão 4.0 está disponível na [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mídia do produto. Você também pode obter a partir de [.NET Framework Developer Center](http://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   Microsoft OLE DB Provider para DB2 versão 5 ou uma versão posterior e a conectividade para os bancos de dados do DB2 que você deseja migrar.  
  
-   Acesso e permissões suficientes no computador que hospeda a instância de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados do SQL Azure onde você irá migrar dados e objetos de banco de dados. Para obter mais informações, consulte [conectando ao SQL Server &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md).  
  
-   4 GB de RAM são recomendados.  
  
## <a name="microsoft-oledb-provider-for-db2"></a>Provedor Microsoft OLEDB para DB2  
Para baixar o provedor OLEDB para DB2 versão 5.0, vá para [Microsoft® SQL Server® 2014 Feature Pack](http://www.microsoft.com/download/details.aspx?id=42295).  
  
O SSMA é um download da Web. Para baixar a versão mais recente, consulte o [página de download do SQL Server Migration Assistant](http://aka.ms/ssmafordb2).  
  
Depois de baixar a versão mais recente, você deve extrair os arquivos de instalação antes de instalar o SSMA.  
  
**Para instalar o cliente do SSMA**  
  
1.  Clique duas vezes o SSMA para DB2 *n*. Install.exe, onde *n* é o número de compilação.  
  
2.  Na página de boas-vinda, clique em **próximo**.  
  
    Se você não tiver os pré-requisitos instalados, será exibida uma mensagem que indica que você deve primeiro instalar os componentes necessários. Certifique-se de que você tenha instalado todos os pré-requisitos e, em seguida, execute o programa de instalação novamente.  
  
3.  Leia o contrato de licença de usuário final. Se você concordar, selecione **aceito os termos do contrato de licença**e, em seguida, clique em **próximo**.  
  
4.  Na página Escolha o tipo de instalação, clique em **típica**.  
  
5.  Clique em **Instalar**.  
  
> [!IMPORTANT]  
> 1.  Desinstale todas as versões anteriores do SSMA para DB2 antes de instalar a nova versão.  
  
O local de instalação padrão é C:\Program Files\Microsoft SQL Server Migration Assistant para DB2.  
  
## <a name="see-also"></a>Consulte também  
[Instalando componentes do SSMA no SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
[Bancos de dados DB2 migrando para o SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
