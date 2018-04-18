# interview

```java


    /**
     * Write a function  merge(head1, head2, head3)
     * that merge given three linked lists in the following way
     * @param head1 Head of first list
     * @param head2 Head of second list
     * @param head3 Head of third list
     * @return list like below
     *
     * [1] -> [2] -> [3]   first list head1 = [1]
     * [A] -> [B] -> [C]   second list head2 = [2]
     * [@] -> [$] -> [%]   third list  head3 = [3]
     *
     * [1] -> [A] -> [@] -> [2] -> [B] -> [$] -> [3] -> [C] -> [%]
     */
    
     
class ListTransformation {

    //Like in C equivalent of struct Node { ...
    class Node {
        Node next;
        String value;

        @Override
        public String toString() {
            return "Node{" +
                    "next=" + next +
                    ", value='" + value + '\'' +
                    '}';
        }
    }


    /**
     *
     * @param head1 Head of first list
     * @param head2 Head of second list
     * @param head3 Head of third list
     * @return list like below
     *
     * [1] -> [2] -> [3]
     * [A] -> [B] -> [C]
     * [@] -> [$] -> [%]
     *
     * [1] -> [A] -> [@] -> [2] -> [B] -> [$] -> [3] -> [C] -> [%]
     */
    Node transformList(Node head1, Node head2, Node head3) {

        Node p_curr1 = head1; Node p_curr2 = head2; Node p_curr3 = head3;
        Node p_next1 = null; Node p_next2 = null; Node p_next3 = null;


        Node ret;
        if(p_curr1 != null)
            ret = p_curr1;
        else if(p_curr2 != null)
            ret = p_curr2;
        else
            ret = p_curr3;

        while (p_curr1 != null || p_curr2 != null || p_curr3 != null) {

            if(p_curr1 != null)
                p_next1 = p_curr1.next;

            if(p_curr2 != null)
                p_next2 = p_curr2.next;

            if(p_curr3 != null)
                p_next3 = p_curr3.next;


            if(p_curr1 != null && p_curr2 != null)
                p_curr1.next = p_curr2;
            else if(p_curr1 != null)
                p_curr1.next = p_curr3;

            if(p_curr2 != null && p_curr3 != null)
                p_curr2.next = p_curr3;
            else if(p_curr2 != null)
                p_curr2.next = p_next1;


            if(p_next1 != null && p_curr3 != null)
                p_curr3.next = p_next1;
            else if(p_next2 != null && p_curr3 != null)
                p_curr3.next = p_next2;
            else if(p_curr3!=null)
                p_curr3.next = p_next3;

            p_curr1 = p_next1;
            p_curr2 = p_next2;
            p_curr3 = p_next3;

        }



        return ret ;
    }





    //--------------------------- POMOCNICZE METODY DO UTWORZENIA LISTY ------------------------------------------------
    Node listBuilder(String... tab) {
        Node head = null;
        Node tmp = null;
        for(String v: tab) {
            if(head == null) {
                Node node = new Node();
                node.value = v;
                head = node;
                tmp = head;
            } else {
                Node node = new Node();
                node.value = v;
                tmp.next = node;
                tmp = node;
            }

        }
        return head;
    }

    void listPrinter(Node head) {
        Node tmp = head;
        while(tmp != null) {
            System.out.print(tmp.value + " ");
            tmp = tmp.next;
        }
        System.out.println("\n");
    }



    public static void main(String[] args) {

        ListTransformation l = new ListTransformation();
        Node head1 = l.listBuilder("1");
        Node head2 = l.listBuilder("A", "B");
        Node head3 = l.listBuilder("@", "$", "(");

        l.listPrinter(head1);
        l.listPrinter(head2);
        l.listPrinter(head3);

        Node head = l.transformList(head1, head2, head3);
        l.listPrinter(head);

    }
}



```
 
