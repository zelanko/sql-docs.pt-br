---
title: Garantindo espaço suficiente de TempDB | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 67dc3f6bb82799382fa2b65754b3645dd735acab
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51560413"
---
# <a name="ensuring-sufficient-tempdb-space"></a>Garantir espaço suficiente de TempDB
Se ocorrerem erros durante a manipulação [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objetos que precisam de processamento de espaço no Microsoft SQL Server 6.5, talvez você precise aumentar o tamanho do TempDB. (Algumas consultas exigem espaço temporário de processamento; por exemplo, uma consulta com uma cláusula ORDER BY requer uma classificação do **Recordset**, que exige algum espaço temporário.)  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
> [!IMPORTANT]
>  Leia este procedimento antes de executar as ações porque não é tão fácil de reduzir um dispositivo depois que ele é expandido.  
  
> [!NOTE]
>  No padrão Microsoft SQL Server 7.0 e versões posterior, o TempDB é definido para aumentar automaticamente conforme necessário. Portanto, este procedimento só pode ser necessário em servidores executando versões anteriores à 7.0.  
  
### <a name="to-increase-the-tempdb-space-on-sql-server-65"></a>Para aumentar o espaço de TempDB no SQL Server 6.5  
  
1.  Iniciar o Microsoft SQL Server Enterprise Manager, abra a árvore para o servidor e, em seguida, abrir a árvore de dispositivos de banco de dados.  
  
2.  Selecione um dispositivo (físico) para expandir, como o mestre e duas vezes no dispositivo para abrir o **Editar banco de dados do dispositivo** caixa de diálogo.  
  
     Essa caixa de diálogo mostra quanto espaço que os bancos de dados atuais estão usando.  
  
3.  No **tamanho** caixa, aumentar o dispositivo para a quantidade desejada (por exemplo, 50 megabytes (MB) de espaço em disco rígido).  
  
4.  Clique em **alteração agora** para aumentar a quantidade de espaço para o qual pode expandir o TempDB (lógico).  
  
5.  Abrir a árvore de bancos de dados no servidor e, em seguida, clique duas vezes **TempDB** para abrir o **Editar banco de dados** caixa de diálogo. O **banco de dados** guia lista a quantidade de espaço alocada atualmente ao TempDB (**tamanho dos dados**). Por padrão, isso é de 2 MB.  
  
6.  Sob o **tamanho** , clique em **expandir**. Os grafos mostram o espaço disponível e alocado em cada um dos dispositivos físicos. As barras na cor Bordô representam o espaço disponível.  
  
7.  Selecione uma **Log de dispositivo**, como o mestre, para exibir o tamanho disponível na **tamanho (MB)** caixa.  
  
8.  Clique em **expanda agora** para alocar esse espaço para o banco de dados TempDB.  
  
     O **Editar banco de dados** caixa de diálogo exibe o novo tamanho alocado para o TempDB.  
  
 Para obter mais informações sobre esse tópico, procure o arquivo de Ajuda do Microsoft SQL Server Enterprise Manager para "Caixa de diálogo de expansão de banco de dados".  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


