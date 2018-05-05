---
title: Garantir espaço suficiente em TempDB | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- TempDB space in RDS [ADO]
ms.assetid: 09130db1-6248-4234-a1e5-a9c8e1622c06
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c86196fdf0320b5f3cb5028cb7d5db484c4da846
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="ensuring-sufficient-tempdb-space"></a>Garantir espaço suficiente em TempDB
Se ocorrerem erros durante o tratamento de [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objetos que precisam de processamento de espaço no Microsoft SQL Server 6.5, talvez seja necessário aumentar o tamanho do TempDB. (Algumas consultas requerem espaço temporário processamento; por exemplo, uma consulta com uma cláusula ORDER BY requer uma classificação do **registros**, que requer espaço temporário.)  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
> [!IMPORTANT]
>  Leia este procedimento antes de executar as ações porque não é mais fácil reduzir um dispositivo quando ele é expandido.  
  
> [!NOTE]
>  No padrão Microsoft SQL Server 7.0 e versões posterior, o TempDB é definido automaticamente cresça conforme necessário. Portanto, esse procedimento só pode ser necessário em servidores que executam versões anteriores à 7.0.  
  
### <a name="to-increase-the-tempdb-space-on-sql-server-65"></a>Para aumentar o espaço de TempDB no SQL Server 6.5  
  
1.  Iniciar o Microsoft SQL Server Enterprise Manager, abra a árvore para o servidor e, em seguida, abra a árvore de dispositivos de banco de dados.  
  
2.  Selecione um dispositivo (físico) para expandir, como mestre e duas vezes no dispositivo para abrir o **Editar banco de dados do dispositivo** caixa de diálogo.  
  
     Essa caixa de diálogo mostra a quantidade de espaço estão usando os bancos de dados atuais.  
  
3.  No **tamanho** caixa, aumentar o dispositivo para a quantidade desejada (por exemplo, 50 megabytes (MB) de espaço em disco).  
  
4.  Clique em **alteração agora** para aumentar a quantidade de espaço para o qual pode expandir o TempDB (lógico).  
  
5.  Abra a árvore de bancos de dados no servidor e, em seguida, clique duas vezes em **TempDB** para abrir o **Editar banco de dados** caixa de diálogo. O **banco de dados** guia lista a quantidade de espaço alocada atualmente ao TempDB (**tamanho dos dados**). Por padrão, isso é 2 MB.  
  
6.  Sob o **tamanho** de grupo, clique em **expandir**. Os gráficos mostram o espaço disponível e alocado em cada um dos dispositivos físicos. As barras de cor marrom representam o espaço disponível.  
  
7.  Selecione um **dispositivo de Log**, como o mestre, para exibir o tamanho disponível no **tamanho (MB)** caixa.  
  
8.  Clique em **expanda agora** ao alocar esse espaço para o banco de dados TempDB.  
  
     O **Editar banco de dados** caixa de diálogo exibe o novo tamanho alocado para TempDB.  
  
 Para obter mais informações sobre este tópico, procure o arquivo de Ajuda do Microsoft SQL Server Enterprise Manager para "Caixa de diálogo de expansão de banco de dados".  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


