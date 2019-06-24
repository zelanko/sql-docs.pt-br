---
title: Recursos internacionais do JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: bbb74a1d-9278-401f-9530-7b5f45aa79de
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b555568ae93936c1f8659b52ba6bb731e8398e0f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66781660"
---
# <a name="international-features-of-the-jdbc-driver"></a>Recursos internacionais do JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Os recursos de internacionalização do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] incluem o seguinte:  
  
-   Suporte para uma experiência completamente localizada nos mesmos idiomas que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Suporte para as conversões da linguagem Java para dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com distinção de localidade  
  
-   Suporte a idiomas internacionais, independentemente do sistema operacional  
  
-   Suporte para nomes de domínio internacionais (começando com o Microsoft JDBC Driver 6.0 para o SQL Server)  
  
## <a name="handling-of-character-data"></a>Tratando de dados de caractere  
 Dados de caractere no Java são tratados por padrão como Unicode; o objeto de Java **String** representa dados de caracteres Unicode. No driver JDBC, a única exceção a esta regra são os métodos getter e setter de fluxo ASCII que são casos especiais porque usam fluxos de byte com a pressuposição implícita de páginas de código simples e conhecidas (ASCII).  
  
 Além disso, o driver JDBC fornece o **sendStringParametersAsUnicode** propriedade de cadeia de caracteres de conexão. Essa propriedade pode ser usada para especificar que os parâmetros preparados para dados de caracteres sejam enviados como ASCII ou conjunto de caracteres multibyte (MBCS) em vez de Unicode. Para obter mais informações sobre o **sendStringParametersAsUnicode** propriedade de cadeia de caracteres de conexão, consulte [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md).  
  
### <a name="driver-incoming-conversions"></a>Conversões de entrada de driver  
 Os dados de texto em Unicode que vêm do servidor não precisam ser convertidos. Eles são passados diretamente como Unicode. Os dados não Unicode que vêm do servidor são convertidos da página de código para os dados, no nível de coluna ou de banco de dados, para Unicode. O driver JDBC usa as rotinas de conversão da Máquina Virtual Java (JVM) para realizar estas conversões. Estas conversões são executadas em todos os métodos getter de fluxo de caracteres e cadeia de caracteres com tipo.  
  
 Se o JVM não tiver o suporte apropriado à página de código para os dados do banco de dados, o driver JDBC lançará uma exceção de "página de código de XXX sem suporte pelo ambiente Java". Para resolver este problema, instale o suporte completo de caractere internacional exigido para essa JVM. Para obter um exemplo, consulte a documentação de Codificações com Suporte no site da Sun Microsystems.  
  
### <a name="driver-outgoing-conversions"></a>Conversões de saída de driver  
 Os dados de caractere que vão do driver para o servidor podem ser ASCII ou Unicode. Por exemplo, os novos métodos de caractere nacional JDBC 4.0, como os métodos setNString, setNCharacterStream e setNClob das classes [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) e [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) sempre enviam os valores de parâmetro para o servidor em Unicode.  
  
 Por outro lado, os métodos da API de caracteres não nacionais, como os métodos setString, setCharacterStream e setClob das classes [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) e [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) enviam os valores para o servidor em Unicode somente quando a propriedade **sendStringParametersAsUnicode** está definida como "true", que é o valor padrão.  
  
## <a name="non-unicode-parameters"></a>Parâmetros não Unicode  
 Para otimizar o desempenho com **CHAR**, **VARCHAR** ou **LONGVARCHAR** tipo de parâmetros não Unicode, defina o **sendStringParametersAsUnicode** propriedade como "false" da cadeia de conexão e usar os métodos de caractere não nacional.  
  
## <a name="formatting-issues"></a>Problemas de formatação  
 Para data, hora e moedas, toda a formatação com os dados localizados é realizada no nível da linguagem Java usando o objeto Locale; e os vários métodos de formatação para tipos de dados **Date**, **Calendar** e **Number**. Em casos raros em que o JDBC Driver precisar passar dados que fazem distinção de localidade em um formato localizado, o formatador correto é usado com a localidade padrão da JVM.  
  
## <a name="collation-support"></a>Suporte a ordenações  
 O JDBC Driver 3.0 é compatível com todas as ordenações compatíveis com [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e as novas ordenações ou novas versões dos nomes de ordenação do Windows apresentadas no [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
 Para obter mais informações sobre as ordenações, consulte [Suporte a ordenações e a Unicode](https://go.microsoft.com/fwlink/?LinkId=131366) e [Nomes de ordenação do Windows (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=131367) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="using-international-domain-names-idn"></a>Usando nomes de domínio internacionais (IDN)  
 O JDBC Driver 6.0 para o SQL Server dá suporte ao uso de nomes de domínio internacionalizados (IDNs) e pode converter um serverName Unicode para compatível com codificação ASCII (Punycode) quando solicitado durante a conexão.  Se os IDNs forem armazenados no sistema de nome de domínio (DNS) como cadeias de caracteres ASCII no formato Punycode (especificado pela RFC 3490), habilite a conversão do nome do servidor Unicode definindo a propriedade serverNameAsACE como true.  Caso contrário, se o serviço DNS é configurado para permitir o uso de caracteres Unicode, defina a propriedade de serverNameAsACE como falso (padrão).  Para versões anteriores do driver JDBC, também é possível converter o serverName em Punycode usando os métodos [IDN.toASCII do Java](https://docs.oracle.com/javase/8/docs/api/java/net/IDN.html) antes de definir essa propriedade para uma conexão.  
  
> [!NOTE]  
>  A maioria dos softwares de resolvedor escritos para plataformas não Windows baseia-se nos padrões da Internet DSN e, portanto, é mais provável usar o formato Punycode IDNs, enquanto um servidor DNS baseados no Windows em uma rede privada pode ser configurado para permitir o uso de caracteres UTF-8 em uma base por servidor.  Para saber mais detalhes, consulte [Suporte a caracteres Unicode](https://technet.microsoft.com/library/cc738403(v=ws.10).aspx).  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
