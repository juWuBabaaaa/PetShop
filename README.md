package petshop;

public class Link 
{
	private class Node
	{
		private Object data ;
		private Node next ;
		public Node(Object data) {
			this.data = data ;
		}

		public Object getData() {
			return this.data ;
		}
		public Node getNext() {
			return this.next ;
		}
		public void addNode(Node newNode) {
			if (this.next == null)
			{
				this.next =newNode ;
			} else {
				this.next.addNode(newNode) ;
			}
		}
		public void toArrayNode() {
			Link.this.retData[Link.this.foot ++] = this.data ;
			if (this.next != null)
			{
				this.next.toArrayNode() ;
			}
		}
		public boolean containsNode(Object search) {
			if (search .equals(this.data))
			{
				return true ;
			} else {
				if (this.next != null)
				{
					return this.next.containsNode(search) ;
				} else {
					return false ;
				}
			}
		}
		public Object getNode(int index) {
			if (Link.this.foot ++ == index)
			{
				return this.data ;
			} else {
				this.next.getNode(index) ;
			}
			return null ;
		}
		public void removeNode(Node previous, Object data) {
			if (this.data.equals(data)) {
				previous.next = this.next ;
			} else {
				this.next.removeNode(next, data);
			}
		}
	}
	// ---------------------- ����ΪLink�ඨ�� ----------------------//
	private Object [] retData ;
	private int foot = 0 ;
	private Node root ;
	private int count = 0 ;
	public Node getNode() {
		return this.root ;
	}
	public void add(Object data) {
		if (data == null)
		{
			return ;
		}
		Node newNode = new Node(data) ;   //��װ
		if (this.root == null) 
		{
			this.root = newNode ;
		} else {
			this.root.addNode(newNode) ;
		}
		this.count ++ ;
	}
	public int size() {
		return this.count ;
	}
	public boolean isEmpty() {
		return this.root == null && this.count == 0 ;
	}
	public Object [] toArray() {
		if (this.count == 0)
		{
			return null ;
		}
		// ����ָ�����ȵ�����
		// ������һ��Ҫ����Node����д���
		this.retData = new Object[this.count] ;
		this.foot = 0 ;
		this.root.toArrayNode() ;
		return this.retData ;
	}
	public boolean contains(Object search) {
		if (search == null || this.root == null)
		{
			return false ;
		}
		return this.root.containsNode(search) ;
	}
	public Object get(int index) {
		if (index >= this.count)
		{
			return null ;
		}
		this.foot = 0 ;
		return this.root.getNode(index) ;
	}
	public void remove(Object data) {
		if (this.contains(data)) {
			if (this.root.data.equals(data)) {
				this.root = this.root.next ; //������һ�����
			} else {
				this.root.next.removeNode(this.root,data) ;
			}
		}
	}
}
