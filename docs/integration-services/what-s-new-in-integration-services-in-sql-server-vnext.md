---
title: "Novidades do Integration Services no SQL Server vNext | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e26d7884-e772-46fa-bfdc-38567fe976a1
caps.latest.revision: 4
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 3
---
# Novidades do Integration Services no SQL Server vNext
Este tópico descreve os recursos adicionados ou atualizados no [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].

>   [!NOTE] O SQL Server vNext também inclui os recursos do SQL Server 2016 e os recursos adicionados nas atualizações do SQL Server 2016. Para obter informações sobre os novos recursos do SSIS no SQL Server 2016, consulte [Novidades do Integration Services no SQL Server 2016](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md).

## <a name="new-in-ssis-in-sql-server-vnext-ctp-11"></a>Novidades do SSIS no SQL Server vNext CTP 1.1

Não há recursos novos do SSIS no SQL Server vNext CTP 1.1.

## <a name="new-in-ssis-in-sql-server-vnext-ctp-10"></a>Novidades do SSIS no SQL Server vNext CTP 1.0

### <a name="scale-out-for-ssis"></a>Expansão para o SSIS

O recurso de Expansão torna muito mais fácil executar [!INCLUDE[ssIS_md](../includes/ssis-md.md)] em vários computadores. 
   
Após a instalação do Mestre de Expansão e do Trabalho de Expansão, o pacote pode ser distribuído para executar diferentes Trabalhos automaticamente. Se a execução for finalizada inesperadamente, a execução será repetida automaticamente. Além disso, todas as execuções e Trabalhos podem ser gerenciados de forma centralizada usando o Mestre.
   
Para obter mais informações, consulte [Expansão do Integration Services](../integration-services/integration-services-ssis-scale-out.md).
   
### <a name="support-for-microsoft-dynamics-online-resources"></a>Suporte para recursos Online do Microsoft Dynamics

O Gerenciador de Fontes OData e o Gerenciador de Conexões OData agora têm suporte para conexão aos feeds OData do Microsoft Dynamics AX Online e do Microsoft Dynamics CRM Online.
