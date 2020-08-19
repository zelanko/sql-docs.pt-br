---
description: Garantir espaço suficiente de TempDB
title: Garantindo espaço TempDB suficiente | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- TempDB space in RDS [ADO]
ms.assetid: 09130db1-6248-4234-a1e5-a9c8e1622c06
author: rothja
ms.author: jroth
ms.openlocfilehash: a84bec7cbd7a79fadf4ea5b11d486e7daf6aa9ab
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452188"
---
# <a name="ensuring-sufficient-tempdb-space"></a>Garantir espaço suficiente de TempDB
Se ocorrerem erros durante o tratamento de objetos [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) que precisam de espaço de processamento no Microsoft SQL Server 6,5, talvez seja necessário aumentar o tamanho do tempdb. (Algumas consultas exigem espaço de processamento temporário; por exemplo, uma consulta com uma cláusula ORDER BY requer um tipo de **conjunto de registros**, que requer algum espaço temporário.)  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
> [!IMPORTANT]
>  Leia este procedimento antes de executar as ações porque não é tão fácil reduzir um dispositivo depois que ele é expandido.  
  
> [!NOTE]
>  Por padrão, o Microsoft SQL Server 7,0 e posterior, o TempDB é definido para crescer automaticamente conforme necessário. Portanto, esse procedimento só pode ser necessário em servidores que executam versões anteriores a 7,0.  
  
### <a name="to-increase-the-tempdb-space-on-sql-server-65"></a>Para aumentar o espaço de TempDB no SQL Server 6,5  
  
1.  Inicie o Gerenciador de Microsoft SQL Server Enterprise, abra a árvore para o servidor e, em seguida, abra a árvore dispositivos de banco de dados.  
  
2.  Selecione um dispositivo (físico) para expandir, como mestre, e clique duas vezes no dispositivo para abrir a caixa de diálogo **Editar dispositivo de banco de dados** .  
  
     Essa caixa de diálogo mostra quanto espaço os bancos de dados atuais estão usando.  
  
3.  Na caixa **tamanho** , aumente o dispositivo para o valor desejado (por exemplo, 50 megabytes (MB) de espaço em disco rígido).  
  
4.  Clique em **alterar agora** para aumentar a quantidade de espaço que o tempdb (lógico) pode expandir.  
  
5.  Abra a árvore bancos de dados no servidor e clique duas vezes em **tempdb** para abrir a caixa de diálogo **Editar banco de dados** . A guia **banco** de dados lista a quantidade de espaço alocada atualmente para tempdb (**tamanho dos dados**). Por padrão, é 2 MB.  
  
6.  No grupo **tamanho** , clique em **expandir**. Os grafos mostram o espaço disponível e alocado em cada um dos dispositivos físicos. As barras na cor bordô representam o espaço disponível.  
  
7.  Selecione um **dispositivo de log**, como mestre, para exibir o tamanho disponível na caixa **tamanho (MB)** .  
  
8.  Clique em **expandir agora** para alocar esse espaço para o banco de dados tempdb.  
  
     A caixa de diálogo **Editar banco de dados** exibe o novo tamanho alocado para tempdb.  
  
 Para obter mais informações sobre este tópico, pesquise o arquivo de ajuda do Microsoft SQL Server Enterprise Manager para a caixa de diálogo "expandir banco de dados".  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


