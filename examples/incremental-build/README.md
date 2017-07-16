# Demonstration of lifecycle issue when xsd changes

1. Run the java compile task

    gradle compileJava

2. Examine the number, datestamp of java files and classes

    find . \( -name "*.java" -o -name "*.class" \) -exec ls -la "{}" \+

3. Edit the xsd file, commenting out the "HelloResponseType" stanza
   (Place an opening comment on line 11, closing comment on line 17)

    emacs src/main/resources/schema/HelloWorld.xsd

4. Run the java compile task again

    gradle compileJava

5. Examine the number, datestamp of java files and classes again

    find . \( -name "*.java" -o -name "*.class" \) -exec ls -la "{}" \+

The issue is that the old java file HelloResponseType.java still exists, and
therefore a HelloResponseType.class will be freshly generated even though we
removed the HelloResponseType from our xsd file.
