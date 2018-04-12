### <a name="binaryformatter-can-fail-to-find-type-from-loadfrom-context"></a>"BinaryFormatter" kann nicht Typ von LoadFrom-Kontext gefunden

|   |   |
|---|---|
|Details|Ab .NET Framework 4.5, diverse <xref:System.Xml.Serialization.XmlSerializer?displayProperty=name> Änderungen können dazu führen, dass Unterschiede bei der Deserialisierung Verwendung <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=name> beim Deserialisieren von Typen, die in den LoadFrom-Kontext geladen wurden. Diese Änderungen sind aufgrund der neuen Möglichkeiten <xref:System.Xml.Serialization.XmlSerializer?displayProperty=name> lädt nun ein anderes Verhalten bewirkt, wenn ein <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=name> zu einem späteren Zeitpunkt auf diesen Typ Deserialisieren versucht. Der Standardbinder für die Serialisierung sucht den LoadFrom-Kontext, obwohl es in einigen Fällen, die basierend auf dem alten Verhalten des XmlSerializer-Elements gearbeitet haben, möglicherweise nicht automatisch. Aufgrund von Änderungen, wenn ein Typ aus einer Assembly geladen wird, in einem anderen Kontext geladen wird eine <xref:System.IO.FileNotFoundException?displayProperty=name> ausgelöst werden.|
|Vorschlag|Wenn diese Ausnahme angezeigt wird, die <code>Binder</code> Eigenschaft von der <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=name> kann festgelegt werden, um einen benutzerdefinierten Binder, die den richtigen Typ gefunden wird.<pre><code class="language-C#">var formatter = new BinaryFormatter { Binder = new TypeFinderBinder() }&#13;&#10;</code></pre>Und klicken Sie dann das benutzerdefinierte Objekt:<pre><code class="language-C#">public class TypeFinderBinder : SerializationBinder&#13;&#10;{&#13;&#10;private static readonly string s_assemblyName = Assembly.GetExecutingAssembly().FullName;&#13;&#10;&#13;&#10;public override Type BindToType(string assemblyName, string typeName)&#13;&#10;{&#13;&#10;return Type.GetType(String.Format(CultureInfo.InvariantCulture, &quot;{0}, {1}&quot;, typeName, s_assemblyName));&#13;&#10;}&#13;&#10;}&#13;&#10;</code></pre>|
|Bereich|Edge|
|Version|4.5|
|Typ|Laufzeit|
|Betroffene APIs|<ul><li><xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=nameWithType></li><li><xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize(System.IO.Stream)?displayProperty=nameWithType></li><li><xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize(System.IO.Stream,System.Runtime.Remoting.Messaging.HeaderHandler)?displayProperty=nameWithType></li></ul>|
