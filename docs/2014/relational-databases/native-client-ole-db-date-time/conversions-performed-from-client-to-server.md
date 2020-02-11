---
title: Conversões executadas do cliente para o servidor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- conversions [OLE DB], client to server
ms.assetid: 6bb24928-0f3e-4119-beda-cfd04a44a3eb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f09cf15479060e455811fa4b3ffe6df4f9bd14cc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63237961"
---
# <a name="conversions-performed-from-client-to-server"></a>Conversões executadas do cliente para o servidor
  Este tópico descreve conversões de data/hora executadas entre um aplicativo cliente escrito com o OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client e o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (ou posterior).  
  
## <a name="conversions"></a>Conversões  
 Este tópico descreve as conversões feitas no cliente. Se o cliente especificar a precisão de frações de segundo para um parâmetro diferente do definido no servidor, a conversão do cliente pode gerar uma falha, nos casos em que o servidor permitiria o êxito da operação. Em particular, o cliente trata qualquer truncamento de segundos fracionários como um erro, enquanto o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] arredonda os valores temporais para o segundo inteiro mais próximo.  
  
 Se ICommandWithParameters:: SetParameterInfo não for chamado, as associações de DBTYPE_DBTIMESTAMP serão convertidas como `datetime2`se estivessem.  
  
|Para -><br /><br /> De|DBDATE (date)|DBTIME (time)|DBTIME2 (time)|DBTIMESTAMP (smalldatetime)|DBTIMESTAMP (datetime)|DBTIMESTAMP (datetime2)|DBTIMESTAMPOFFSET (datetimeoffset)|STR|WSTR|SQLVARIANT<br /><br /> (sql_variant)|  
|----------------------|---------------------|---------------------|----------------------|-----------------------------------|------------------------------|-------------------------------|------------------------------------------|---------|----------|-------------------------------------|  
|DATE|1,2|1,3,4|4,12|1,12|1,12|1,12|1,5, 12|1,12|1,12|1,12<br /><br /> datetime2(0)|  
|DBDATE|1|-|-|1,6|1,6|1,6|1,5, 6|1,10|1,10|1<br /><br /> date|  
|DBTIME|-|1|1|1,7|1,7|1,7|1,5, 7|1,10|1,10|1<br /><br /> Time(0)|  
|DBTIME2|-|1,3|1|1,7,10,14|1,7,10,15|1,7,10|1,5,7,10|1,10,11|1,10,11|1<br /><br /> Time(7)|  
|DBTIMESTAMP|1,2|1,3,4|1,4,10|1,10,14|1,10,15|1,10|1,5,10|1,10,11|1,10,11|1,10<br /><br /> Datetime2 (7)|  
|DBTIMESTAMPOFFSET|1,2,8|1,3,4,8|1,4,8,10|1,8,10,14|1,8,10,15|1,8,10|1,10|1,10,11|1,10,11|1,10<br /><br /> datetimeoffset(7)|  
|FILETIME|1,2|1,3,4|1,4,13|1,13|1,13|1,13|1,5,13|1,13|1,10|1,13<br /><br /> datetime2(3)|  
|BYTES|-|-|-|-|-|-|-|N/D|N/D|N/D|  
|VARIANT|1|1|1|1,10|1,10|1,10|1,10|N/D|N/D|1,10|  
|SSVARIANT|1,16|1,16|1,16|1,10,16|1,10,16|1,10,16|1,10,16|N/D|N/D|1,16|  
|BSTR|1,9|1,9|1,9,10|1,9,10|1,9,10|1,9,10|1,9,10|N/D|N/D|N/D|  
|STR|1,9|1,9|1,9,10|1,9,10|1,9,10|1,9,10|1,9,10|N/D|N/D|N/D|  
|WSTR|1,9|1,9|1,9,10|1,9,10|1,9,10|1,9,10|1,9,10|N/D|N/D|N/D|  
  
## <a name="key-to-symbols"></a>Legenda dos símbolos  
  
|Símbolo|Significado|  
|------------|-------------|  
|-|Não há suporte a nenhuma conversão. Se a associação for validada quando IAccessor:: createaccess for chamado, DBBINDSTATUS_UPSUPPORTEDCONVERSION será retornado em *rgStatus*. Quando a validação de acessador for adiada, DBSTATUS_E_BADACCESSOR será definido.|  
|N/D|Não aplicável.|  
|1|Se os dados fornecidos não forem válidos, DBSTATUS_E_CANTCONVERTVALUE será definido. Os dados de entrada são validados antes da aplicação das conversões; assim, mesmo quando um componente for ignorado por uma conversão subsequente, ele ainda deverá ser válido para que a conversão tenha êxito.|  
|2|Os campos de hora são ignorados.|  
|3|As frações de segundo devem ser zero ou DBSTATUS_E_DATAOVERFLOW será definido.|  
|4|O componente de data é ignorado.|  
|5|O fuso horário é definido com a configuração de fuso horário do cliente.|  
|6|A hora é definida como zero.|  
|7|A data é definida com a data atual.|  
|8|A hora é convertida a UTC. Se ocorrer um erro durante essa conversão, DBSTATUS_E_CANTCONVERTVALUE será definido.|  
|9|A cadeia de caracteres é analisada como um literal ISO e convertida para o tipo de destino. Se houver falha, a cadeia de caracteres será analisada como um literal de data OLE (que também tem componentes de hora) e convertida de uma data OLE (DBTYPE_DATE) para o tipo de destino.<br /><br /> Se o tipo de destino for DBTIMESTAMP, `smalldatetime`, `datetime` ou `datetime2`, a cadeia de caracteres deverá estar de acordo com a sintaxe de data, hora ou literais `datetime2`, ou com a sintaxe reconhecida pelo OLE. Se a cadeia de caracteres for um literal de data, todos os componentes de hora serão definidos como zero. Se a cadeia de caracteres for um literal de hora, a data será definida com a data atual.<br /><br /> Para todos os outros tipos de destino, a cadeia de caracteres deve estar de acordo com a sintaxe de literais do tipo de destino.|  
|10|Se ocorrer o truncamento de frações de segundo com perda de dados, DBSTATUS_E_DATAOVERFLOW será definido. Para conversões de cadeia de caracteres, a verificação de estouro é possível somente quando a cadeia de caracteres estiver de acordo com a sintaxe ISO. Se a cadeia de caracteres for um literal de data OLE, as frações de segundo serão arredondadas.<br /><br /> Para conversão de DBTIMESTAMP (datetime) em smalldatetime, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client truncará silenciosamente o valor de segundos, em vez de gerar o erro DBSTATUS_E_DATAOVERFLOW.|  
|11|O número de dígitos das frações de segundo (a escala) é determinado pelo tamanho da coluna de destino, de acordo com a seguinte tabela. Para tamanhos de coluna maiores do que o intervalo na tabela, é sugerida uma escala de 9. Essa conversão deve permitir até nove dígitos de frações de segundo, o máximo permitido pelo OLE DB.<br /><br /> Porém, se o tipo de origem for DBTIMESTAMP e as frações de segundo forem zero, não serão gerados dígitos de fração de segundo ou vírgulas decimais. Este comportamento assegura a compatibilidade com versões anteriores de aplicativos desenvolvidos usando provedores OLE DB mais antigos.<br /><br /> Um tamanho de coluna de ~ 0 implica em tamanho ilimitado no OLE DB (9 dígitos, a menos que a regra de 3 dígitos para DBTIMESTAMP se aplique).<br /><br /> **DBTIME2** -8, 10.. 18 (comprimento em caracteres); 0, 1.. 9 (escala)<br /><br /> **DBTIMESTAMP** -19, 21.. 29 (comprimento em caracteres); 0, 1.. 9 (escala)<br /><br /> **DBTIMESTAMPOFFSET** -26, 28.. 36 (comprimento em caracteres); 0, 1.. 9 (escala)|  
|12|A semântica de conversão anterior ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] para DBTYPE_DATE é mantida. As frações de segundo são truncadas para zero.|  
|13|A semântica de conversão anterior ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] para DBTYPE_FILETIME é mantida. Se você usar a API FileTimeToSystemTime do Windows, a precisão de segundos fracionários estará limitada a 1 milissegundo.|  
|14|A semântica de conversão anterior ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] para `smalldatetime` é mantida. Os segundos são definidos como zero.|  
|15|A semântica de conversão anterior ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] para `datetime` é mantida. Os segundos são arredondados para o 300º de segundo mais próximo.|  
|16|O comportamento de conversão de um valor (de um tipo determinado) inserido em uma estrutura cliente SSVARIANT é igual ao comportamento do mesmo valor e tipo quando não inserido em uma estrutura cliente SSVARIANT.|  
  
## <a name="see-also"></a>Consulte Também  
 [Associações e conversões &#40;OLE DB&#41;](conversions-ole-db.md)  
  
  
