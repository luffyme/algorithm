        二叉搜索树
            二叉搜索树（英语：Binary Search Tree），也称二叉搜索树、有序二叉树（英语：ordered binary tree），排序二叉树（英语：sorted binary tree），
            是指一棵空树或者具有下列列性质的二叉树：
                1. 若任意节点的左子树空，则左子树上所有结点的值均小于它的根结点的值；
                2. 若任意节点的右子树空，则右子树上所有结点的值均大于它的根结点的值；
                3. 任意节点的左、右子树也分别为二叉查找树。
            
            https://leetcode-cn.com/problems/validate-binary-search-tree
				func isValidBST(root *TreeNode) bool {
					return valid(root, math.MinInt64, math.MaxInt64)
				}

				func valid(root *TreeNode, min, max int) bool {
					if root == nil {
						return true
					}

					if root.Val >= max || root.Val <= min {
						return false
					}

					return valid(root.Left, min, root.Val) && valid(root.Right, root.Val, max)
				}
			
            https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-search-tree/
            https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/