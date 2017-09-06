---
title: "Implementando uma classe DataReader para uma extensão de processamento de dados | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- data processing extensions [Reporting Services], data readers
- data readers [Reporting Services]
- DataReader class
- read-only data
ms.assetid: 23e286e7-6074-4fbe-be29-203420d6c3d0
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: cfd3a6cb38c59b1810d046839cb3be4f0dc9846a
ms.contentlocale: pt-br
ms.lasthandoff: 08/12/2017

---
# <a name="implementing-a-datareader-class-for-a-data-processing-extension"></a>Implementando uma classe DataReader para uma extensão de processamento de dados
  O **DataReader** objeto permite que um cliente recuperar um fluxo de dados somente leitura, somente encaminhamento de uma fonte de dados. Os resultados são retornados como a consulta é executada e são armazenados no buffer de rede no cliente até que você os solicite usando o **leitura** método o **DataReader** classe. Para criar um **DataReader** classe, implemente <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> e, opcionalmente, implemente <xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension>. Usando um **DataReader** objeto aumenta o desempenho do aplicativo ao recuperar dados assim que ele estiver disponível, em vez de aguardar por todos os resultados da consulta a ser retornada e (por padrão) armazenar somente uma linha por vez na memória, reduzindo a sobrecarga do sistema.  
  
 Depois de criar uma instância do seu **comando** classe, você cria um **DataReader** objeto chamando **ExecuteReader** para recuperar linhas da fonte de dados. O **DataReader** implementação deverá fornecer dois recursos básicos: acesso somente de encaminhamento de resultados define obtido executando um comando e acesso para os tipos de coluna, nomes e valores em cada linha. Os clientes usam o **leitura** método o **DataReader** para obter uma linha dos resultados da consulta.  
  
 No Designer de relatórios, sua **DataReader** objeto é usado para recuperar uma lista de campos, bem como informações de esquema sobre o conjunto de resultados. Isso é realizado pela implementação de **GetName**, **GetValue**, **GetFieldType** e **GetOrdinal** métodos do <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> interface.  
  
 A interface de <xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension> permite que você ofereça informações específicas de agregação sobre o seu conjunto de resultados. Para obter um exemplo **DataReader** implementação da classe, consulte [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Consulte também  
 [Extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementando uma extensão de processamento de dados](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
